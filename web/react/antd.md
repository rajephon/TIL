# antd

## Upload.Dragger 에서 파일 선택 시 곧바로 AJAX 호출하지 않게 하려면

- `beforeUpload` 콜백에서 `false`로 응답한다.

```typescript
ReactDOM.render(
    <Upload.Dragger beforeUpload={() => false} />
);

// or

const beforeUpload = (file:RcFile) {
    console.log(file.text());
    return false;
}
ReactDOM.render(
    <Upload.Dragger beforeUpload={beforeUpload} />
);
```

- 혹은 `customRequest` 속성을 활용할 수도 있다.

```typescript
const dummyRequest = ({ file, onSuccess }:RcCustomRequestOptions) => {
  setTimeout(() => {
    onSuccess("ok");
  }, 0);
};
ReactDOM.render(
    <Upload.Dragger customRequest={dummyRequest} />
);
```

## Reference

- [action function is required with antd upload control, but I dont need it - Stack overflow](https://stackoverflow.com/a/51519603)
- [Upload files manually after beforeUpload returns false. - antd](https://ant.design/components/upload/#components-upload-demo-upload-manually)

