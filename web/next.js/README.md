## next-auth ERR_PACKAGE_PATH_NOT_EXPORTED 오류 발생 시

```
error - Error [ERR_PACKAGE_PATH_NOT_EXPORTED]: Package subpath './providers/credentials' is not defined by "exports" in foo/bar/node_modules/next-auth/package.json
error - Error [ERR_PACKAGE_PATH_NOT_EXPORTED]: Package subpath './providers/credentials' is not defined by "exports" in foo/bar/node_modules/next-auth/package.json
```

### 해결
- node 버전을 올리면 해결된다.
```bash
$ node --version
v12.18.0
$ npm cache clean -f 
$ npm install -g n
$ sudo n stable
 installing : node-v16.13.1
       mkdir : /usr/local/n/versions/node/16.13.1
       fetch : https://nodejs.org/dist/v16.13.1/node-v16.13.1-darwin-x64.tar.xz
   installed : v16.13.1 (with npm 8.1.2)

```

## next.js 어플리케이션 도커라이즈

[Docker multi-stage build](https://docs.docker.com/develop/develop-images/multistage-build/)를 이용하여 이미지 크기를 가능한 한 작게 만들고, 필요한 것들만 포함하도록 작성해보자. 

### Dockerfile
```

FROM node:lts-alpine as dependencies
WORKDIR /my-project
COPY package*.json ./
RUN npm install

FROM node:lts-alpine as builder
WORKDIR /my-project
COPY . .
COPY --from=dependencies /my-project/node_modules ./node_modules
RUN npm run build

FROM node:lts-alpine as runner
WORKDIR /my-project
ENV NODE_ENV production
# If you are using a custom next.config.js file, uncomment this line.
# COPY --from=builder /my-project/next.config.js ./
COPY --from=builder /my-project/public ./public
COPY --from=builder /my-project/.next ./.next
COPY --from=builder /my-project/node_modules ./node_modules
COPY --from=builder /my-project/package.json ./package.json

EXPOSE 3000
CMD ["npm", "start"]
```

- 첫 번째 스테이지에서는 디펜던시를 설치하고,
- 두 번째 스테이지에서는 Next.js 앱을 빌드하고,
- 세 번째 스테이지에서는 Next.js 앱의 런타임 환경을 구성한다.

그리고 다음의 명령어로 도커 이미지를 빌드

```
docker build --tag my-project:0.1 .
```


그리고 포트를 매핑하며 실행한다.
```
docker run -p 3000:3000 my-project:0.1
```

### Reference
- [How to Dockerize and Deploy a Next.js Application on Koyeb](https://www.koyeb.com/tutorials/how-to-dockerize-and-deploy-a-next-js-application-on-koyeb)

## 커스텀 에러 페이지

- 서버 처리중 오류 발생할 경우 표시
- `_error.tsx` 파일명으로 페이지 생성

### 예시

```typescript
import React from 'react'
import { NextPageContext } from 'next';
import Image from 'next/image'
import { Alert } from 'antd';

interface ErrorComponentProps {
  statusCode: number;
  errorMessage?: string;
}


function ErrorComponent({ statusCode, errorMessage }:ErrorComponentProps): JSX.Element {
  return <>
    <h1>{statusCode}</h1>
    <Image src={`https://http.cat/${statusCode}`} alt="Error" width={750} height={600} />
    {errorMessage && <div style={{display: 'block'}}>
      <Alert
        message={`ERROR: ${statusCode}`}
        description={errorMessage}
        type="error"
        showIcon
      />
    </div> }
  </>
}


ErrorComponent.getInitialProps = ({ res, err }:NextPageContext) => {
  const statusCode = res ? res.statusCode : err ? err.statusCode : 404
  return { statusCode }
}


export default ErrorComponent;

```


## `<title>`은 `_document.js`의 `<Head>`에서 쓰지 말 것.

- `_document.js`는 초기 pre-render 에서만 렌더링되기 때문에 `next/head`에서 예기치 못한 결과를 가져올 수 있다.
- 예시: 각 페이지에서 `<title>`을 덧씌우고 브라우저 개발자 도구로 확인해보면 `<title>` 태그가 두 개가 들어있다던가, 등


### 대안

- `_app.js`를 사용하자.

```typescript
import { AppProps } from 'next/app'
import Head from 'next/head'

function MyApp({ Component, pageProps: { session, ...pageProps } }: AppProps) {
  return (
    <>
      <Head>
        <title>Hello World</title>
      </Head>
      <SessionProvider session={session}>
        <Component {...pageProps} />
      </SessionProvider>
    </>
  )
}
```

### References

- [`<title>` should not be used in _document.js's `<Head>`](https://nextjs.org/docs/messages/no-document-title)

