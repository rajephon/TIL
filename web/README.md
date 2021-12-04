# Web

## 이모지를 파비콘으로 사용 하려면?

### 방법1

```html
<link rel="icon" href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><text y=%22.9em%22 font-size=%2290%22>🎉</text></svg>">
```

### 방법2

다음과 같이 `favicon.svg` 파일을 별도로 만들고 연결해준다.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100">
    <text y=".9em" font-size="90">🌳</text>
</svg>
```

```html
<link rel="icon" href="%PUBLIC_URL%/favicon.svg" />
```

### Reference

- https://twitter.com/LeaVerou/status/1241619866475474946
- [Emojis as Favicons - CSS-Tricks](https://css-tricks.com/emojis-as-favicons/)