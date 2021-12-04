# React

## 10,000개가 넘는 아이템을 빠르게 렌더링하는 방법?
- 10,000개가 넘는 모든 것들 렌더링 하지 말 것.
  - 줄일 수 있는 만큼 최대한 줄이는 게 가장 좋음.
  - `InfiniteScroll`처럼 보이는 것들만 렌더링 해서 눈속임을 하는게 가장 효율적이다.
- 미세 최적화(micro-optimize)
  - storage.toArray().map(...)을 사용하여 중간 맵 없이 바로 처리한다거나,
  - 혹은 빈 배열을 만들고 storage.forEach(...)로 엘리먼트를 넣는다거나,
  - 하지만 이 모든 것들도 React diffing algorithm이 10,000개가 넘는 요소를 비교해야 하기 때문에 결코 빠르지 않다.
- 최대한 청크 단위로 분할한다. 마찬가지로 컴포넌트도 쪼갤 수 있는 만큼 쪼개서 특정 요소가 변경되면 해당 청크만 다시 렌더링 되도록 한다.
- `React.useMemo`로 컴포넌트 리렌더링 방지

### Reference

- [How to fast render >10000 items using React + Flux? - Stack Overflow](https://stackoverflow.com/a/33962142)


## 리액트 렌더링이 끝날 때까지 로딩스크린을 보여주는 방법

- `public/index.html`의 리액트 엘리먼트 트리를 렌더링 할 div 안에 렌더 전 나타날 요소들을 기록하면 된다.
<details>
<summary>Example Code</summary>
<div markdown="1">

```html
<head>
    <title>React App</title>
    <style>
      #root .loader-container {
        background-color: #0cbaba;
        background-image: linear-gradient(315deg, #0cbaba 0%, #380036 74%);
        height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
      }

      #root {
        /* display: none; */
      }
      .sk-chase {
        width: 40px;
        height: 40px;
        position: relative;
        animation: sk-chase 2.5s infinite linear both;
      }

      .sk-chase-dot {
        width: 100%;
        height: 100%;
        position: absolute;
        left: 0;
        top: 0;
        animation: sk-chase-dot 2s infinite ease-in-out both;
      }

      .sk-chase-dot:before {
        content: "";
        display: block;
        width: 25%;
        height: 25%;
        background-color: #fff;
        border-radius: 100%;
        animation: sk-chase-dot-before 2s infinite ease-in-out both;
      }

      .sk-chase-dot:nth-child(1) {
        animation-delay: -1.1s;
      }
      .sk-chase-dot:nth-child(2) {
        animation-delay: -1s;
      }
      .sk-chase-dot:nth-child(3) {
        animation-delay: -0.9s;
      }
      .sk-chase-dot:nth-child(4) {
        animation-delay: -0.8s;
      }
      .sk-chase-dot:nth-child(5) {
        animation-delay: -0.7s;
      }
      .sk-chase-dot:nth-child(6) {
        animation-delay: -0.6s;
      }
      .sk-chase-dot:nth-child(1):before {
        animation-delay: -1.1s;
      }
      .sk-chase-dot:nth-child(2):before {
        animation-delay: -1s;
      }
      .sk-chase-dot:nth-child(3):before {
        animation-delay: -0.9s;
      }
      .sk-chase-dot:nth-child(4):before {
        animation-delay: -0.8s;
      }
      .sk-chase-dot:nth-child(5):before {
        animation-delay: -0.7s;
      }
      .sk-chase-dot:nth-child(6):before {
        animation-delay: -0.6s;
      }

      @keyframes sk-chase {
        100% {
          transform: rotate(360deg);
        }
      }

      @keyframes sk-chase-dot {
        80%,
        100% {
          transform: rotate(360deg);
        }
      }

      @keyframes sk-chase-dot-before {
        50% {
          transform: scale(0.4);
        }
        100%,
        0% {
          transform: scale(1);
        }
      }
    </style>
</head>
<body>
<noscript>
    You need to enable JavaScript to run this app.
</noscript>
<div id="root">
    <div class="loader-container">
    <div class="loader">
        <div class="sk-chase">
        <div class="sk-chase-dot"></div>
        <div class="sk-chase-dot"></div>
        <div class="sk-chase-dot"></div>
        <div class="sk-chase-dot"></div>
        <div class="sk-chase-dot"></div>
        <div class="sk-chase-dot"></div>
        </div>
    </div>
    </div>
</div>
</body>
```

</div>
</details>


### Reference
- [Example](https://codesandbox.io/s/silly-frog-z7ju3)
- [How to have a loading screen until all my components are mounted in React - Stack Overflow](https://stackoverflow.com/questions/66136068/how-to-have-a-loading-screen-until-all-my-components-are-mounted-in-react)

## 리액트에서 10,000개가 넘는 마커를 지도 위에 표시하기
- 대부분 지도 API는 마커와 여러 마커를 뭉쳐 표시할 수 있는 마커 클러스터가 있음.
- 하지만 대부분의 지도 및 지도 라이브러리들은 일정 개수 이상의 마커가 표시되면 렌더링 이슈가 발생
  - 마커 클러스터를 넣을 경우, 마커를 child component 형태로 가져오므로, 데이터가 많을 경우 최초 로드 시 렌더링이 매우 매우 느림
  - [Leaflet](https://leafletjs.com/), [React Google Maps API](https://github.com/JustFly1984/react-google-maps-api) 등 모두 마찬가지
- 해결책으로, [캔버스를 그리고 그 위에다가 구현하는 방법](https://github.com/istarkov/google-map-thousands-markers)도 있지만,
- 그냥 편한길을 가자. 데이터가 많을 경우 [맵박스](https://www.mapbox.com/) 가 매우 유리함
