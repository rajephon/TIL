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