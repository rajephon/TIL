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

### Reference

- [action function is required with antd upload control, but I dont need it - Stack overflow](https://stackoverflow.com/a/51519603)
- [Upload files manually after beforeUpload returns false. - antd](https://ant.design/components/upload/#components-upload-demo-upload-manually)


## 상단 메뉴바 아이템 좌우 배치하기

메뉴바 아이템을 좌, 우로 나눠 배치하려면 속성값을 사용한 정렬은 없고, CSS를 이용해야 한다.

```typescript

import React, {CSSProperties} from "react";

const centerStyle:CSSProperties = {
  position: 'relative',
  display: 'flex',
  justifyContent: 'left',
};

const rightStyle:CSSProperties = {
  position: 'absolute',
  top: 0,
  right: 0
};

const HeaderTest:React.FC = () => {
  return (
    <Header>
      <Menu theme="dark" mode="horizontal" style={centerStyle}>
        <Menu.Item key='1'>1</Menu.Item>
        <Menu.Item key='2'>2</Menu.Item>
      </Menu>
      <Menu theme="dark" mode="horizontal" style={rightStyle}>
        <Menu.Item key='3'>3</Menu.Item>
        <Menu.Item key='4'>4</Menu.Item>
      </Menu>
    </Header>
  );
};

export default HeaderTest;
```

### Reference

- [Menu item grouping and alignment](https://github.com/ant-design/ant-design/issues/10749#issuecomment-614181734)