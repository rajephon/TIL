# Mapbox

## 내 위치 트래킹 및 표시하기

```typescript
import ReactMapGL, {GeolocateControl} from 'react-map-gl';

const MapArea:React.FC = ():React.ReactElement => {
    return (
        <ReactMapGL>
            <GeolocateControl
                    positionOptions={{enableHighAccuracy: true}}
                    showUserLocation={true}
                    trackUserLocation={false}
                    fitBoundsOptions={{maxZoom: 15}}
                    />
        </ReactMapGL>
    );
}
```

- showUserLocation
    - 내 위치(파란 점) 표시 여부
- trackUserLocation
    - 지속 탐색 옵션(화면이 따라간다)
- fitBoundsOptions
    사용자 위치로 자동 이동 및 확대/축소될 때 나타나는 [fitbound](https://visgl.github.io/react-map-gl/docs/api-reference/web-mercator-viewport#fitboundsbounds-options-object)의 옵션. 기본값은 `{maxZoom: 15}` 이며, 사용자 위치로 이동된 뒤 나타나는 최대 줌 수치.


### References
- [geolocate-control - mapbox docs](https://visgl.github.io/react-map-gl/docs/api-reference/geolocate-control)