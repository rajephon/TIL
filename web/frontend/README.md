# 웹 프론트엔드

## 모바일 여부 확인 방법

### TL;DR

```javascript
const isMobileOS = /iPhone|iPad|iPod|Android/i.test(navigator.userAgent);
```

### 다른 방법

[react-device-detect](https://github.com/duskload/react-device-detect) 패키지를 설치해 이용하는 방법도 있다.

```javascript
import {BrowserView, MobileView} from 'react-device-detect';

const MyComponent = () => {
    return (
        <>
            <BrowserView>
                <h1>This is rendered only in browser</h1>
            </BrowserView>
            <MobileView>
                <h1>This is rendered only on mobile</h1>
            </MobileView>
        </>
    );
};
```

혹은

```javascript
import {isMobile} from 'react-device-detect';

const MyComponent = () => {
    if(isMobile) {
        return (
            <div> This content is available only on mobile</div>
        )
    }
    return (
        <div> content... </div>
    );
};
```

- 복잡하게 쓸거 아니면 종속 추가하지 말고 그냥 UA 에서 regex 파싱 한 줄로 끝내는게 편할듯.

- 구체적으로 UA를 파싱해 분류하려면 [ua-parser-js](https://github.com/faisalman/ua-parser-js)
  

#### References
- https://github.com/faisalman/ua-parser-js
- https://stackoverflow.com/a/60932511
- https://github.com/duskload/react-device-detect



## 썸네일을 위한 메타 데이터

### Open Graph protocol
- 많은 값들이 있지만, 일단 당장 쓰는 것들로 보면,
```html
    <meta property="og:type" content="website" />
    <meta property="og:url" content="%PUBLIC_URL%" />
    <meta property="og:title" content="사이트 제목" />
    <meta property="og:image" content="썸네일 이미지 url" />
    <meta property="og:description" content="사이트 설명" />
    <meta property="og:locale" content="ko_KR" />
```


### 트위터
```html
    <meta name="twitter:card" content="summary_large_image" />
    <meta name="twitter:title" content="사이트 제목" />
    <meta name="twitter:description" content="사이트 설명" />
    <meta name="twitter:image" content="사이트 썸네일" />
```
- 썸네일 이미지 주소는 절대주소를 사용한다.
  - 리액트에서 `%PUBLIC_URL%`의 값이 공백으로 나타날 경우, `package.json`에 `homepage`값 지정여부 확인 및 .nev 파일에 `PUBLIC_URL` 를 환경변수 형태로 추가해준다.
  

### 테스트
- 일반웹: [https://www.heymeta.com/](https://www.heymeta.com/)
- 트위터: [https://cards-dev.twitter.com/validator](https://cards-dev.twitter.com/validator)
- 카카오톡 서비스: [https://developers.kakao.com/tool/clear/og](https://developers.kakao.com/tool/clear/og)
