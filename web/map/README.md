# Map

## 지도 바로가기

### 네이버 지도

```text
https://map.naver.com/?query=${주소}
```
혹은
```text
https://map.naver.com/v5/?c={X좌표},{Y좌표},{줌레벨},0,0,0,dh&lng=경도&lat=위도&type=0&title=위치이름
```

- XY좌표계는 EPSG:3857
- 모바일에서 앱 연결 시 위치가 같이 표시되지 않는 문제가 있다.


### 네이버 지도 앱으로 연결

```
nmap://place?lat={위도}&lng={경도}&name={위치이름}&appname=com.example.myapp
```

### 카카오 맵

```text
https://map.kakao.com/link/map/{이름},{위도},{경도}
```

### Reference
- [Google Map, Naver Map URL 만들기 ](https://jehyunlee.github.io/2020/04/15/GIS-Python-1-GoogleMapNaverMap/)
- [네이버 지도앱 연동 URL Scheme](https://guide.ncloud-docs.com/docs/naveropenapiv3-maps-url-scheme-url-scheme)
- [Kakao 지도 Web API 가이드](https://apis.map.kakao.com/web/guide/)