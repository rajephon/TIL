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