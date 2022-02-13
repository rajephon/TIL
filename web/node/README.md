# node.js

## node-fetch

- node-fetch v3 부터는 __ESM-only module__
- `require()` 로 임포트가 불가하다.
- ESM으로 전환이 불가능할 경우 크리티컬한 버그 수정은 계속 해줄 예정이므로 v2를 사용할 것

```
npm install node-fetch@2
```

- 혹은 async `import()` 를 이용해 로드할 수도 있다.

```javascript
// mod.cjs
const fetch = (...args) => import('node-fetch').then(({default: fetch}) => fetch(...args));
```

### References

- [Loading and configuring the module - node-fetch](https://github.com/node-fetch/node-fetch#commonjs)

