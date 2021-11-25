# React

## 10,000개가 넘는 아이템을 빠르게 렌더링하는 방법?
- 10,000개가 넘는 모든 것들 렌더링하지 말것.
  - 줄일 수 있는 만큼 최대한 줄이는게 가장 좋음.
  - `InfiniteScroll` 처럼 보이는 것들만 렌더링해서 눈속임을 하는게 가장 효율적이다.
- 미세 최적화(micro-optimize)
  - storage.toArray().map(...)을 사용하여 중간맵 없이 바로 처리한다거나,
  - 혹은 빈 배열을 만들고 storage.forEach(...)로 엘리먼트를 넣는다거나,
  - 하지만 이 모든 것들도 React diffing algorithm이 10,000개가 넘는 요소를 비교해야 하기 때문에 결코 빠르지 않다.
- 최대한 청크단위로 분할한다. 마찬가지로 컴포넌트도 쪼갤 수 있는 만큼 쪼개서 특정 요소가 변경되면 해당 청크만 다시 렌더링되도록 한다.
- `React.useMemo`로 컴포넌트 리렌더링 방지

### Reference

- [How to fast render >10000 items using React + Flux? - Stack Overflow](https://stackoverflow.com/a/33962142)


## 리액트 렌더링이 끝날 때까지 로딩스크린을 보여주는 방법



### Reference
- [Example](https://codesandbox.io/s/silly-frog-z7ju3)
- [How to have a loading screen until all my components are mounted in React - Stack Overflow](https://stackoverflow.com/questions/66136068/how-to-have-a-loading-screen-until-all-my-components-are-mounted-in-react)




https://stackoverflow.com/questions/66136068/how-to-have-a-loading-screen-until-all-my-components-are-mounted-in-react

https://codesandbox.io/s/silly-frog-z7ju3?file=/src/index.js:288-438

root 사이에 그려놓기 (render 끝나면 덮어씌워진다)

return (
    isLoading ? "Loading…" : elements
)


https://leafletjs.com/

리액트에서 google maps나 leaflet은 marker cluster를 넣을 경우, marker를 child component 형태로 가져오므로, 데이터가 많을 경우 최초 로드시 렌더링이 매우 매우 느림

https://stackoverflow.com/questions/33959737/how-to-fast-render-10000-items-using-react-flux
Don't render all 10,000 -

캔버스를 그리고 그 위에다가 구현하는 방법도 있지만, 그냥 편한길을 가자. 데이터가 많을 경우 맵박스가 매우 유리함(애초에 용도가 그런 용도길래)