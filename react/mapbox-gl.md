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


### Reference
- [geolocate-control - mapbox docs](https://visgl.github.io/react-map-gl/docs/api-reference/geolocate-control)


## 팝업 띄우기

```javascript
import * as React from 'react';
import ReactMapGL, {Popup} from 'react-map-gl';

function App() {
  const [viewport, setViewport] = React.useState({
    longitude: -122.45,
    latitude: 37.78,
    zoom: 14
  });
  const [showPopup, togglePopup] = React.useState(false);

  return (
    <ReactMapGL {...viewport} width="100vw" height="100vh" onViewportChange={setViewport}>
      {showPopup && <Popup
          latitude={37.78}
          longitude={-122.41}
          closeButton={true}
          closeOnClick={false}
          onClose={() => togglePopup(false)}
          anchor="top" >
          <div>You are here</div>
        </Popup>}
    </ReactMapGL>
  );
}
```

### circle Layer 선택 시 팝업 띄우기

```typescript
type PopupInfo = {
    latitude: number;
    longitude: number;
};

const MapArea = () => {
    const [popupInfo, setPopupInfo] = React.useState<PopupInfo|null>(null);

    const onClick = (event:MapEvent) => {
        if (!event.features) {
            console.error("event.features is undefined");
            return;
        }
        if (!mapRef.current) {
            console.error("mapRef.current is undefined");
            return;
        }
        if (event.features.length === 0) {
            console.error("event.features.length === 0");
            return;
        }
        const feature = event.features[0];
        const newPopupInfo:PopupInfo = {
            latitude: feature.geometry.coordinates[1],
            longitude: feature.geometry.coordinates[0],
        };
        setPopupInfo(newPopupInfo);
    };

    return (
        <ReactMapGL
            onClick={onClick}>
            {popupInfo && (
                <Popup longitude={popupInfo.longitude} latitude={popupInfo.latitude} onClose={() => {setPopupInfo(null)}} closeButton={true}>
                    <div>
                        <h3>Hello</h3>
                    </div>
                </Popup>
            )}
            <Source id={sourceId} type={'geojson'} data={{type: "FeatureCollection", features: features}}  
                    cluster={true} clusterMaxZoom={14}>
                    ...
                    <Layer id='unclustered-point' source={sourceId}
                       type={'circle'} filter={['!', ['has', 'point_count']]}
                       paint={{'circle-color': '#11b4da', 'circle-radius': 5, 'circle-stroke-width': 1, 'circle-stroke-color': '#fff'}} />
            </Source>
        </ReactMapGL>
    )
};
```

### Reference
- [Popup - react-map-gl](https://visgl.github.io/react-map-gl/docs/api-reference/popup)