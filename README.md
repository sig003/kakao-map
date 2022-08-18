# kakao-map
```
//작업 전 카카오 디벨로퍼스에서 내 애플리케이션>앱 설정>플랫폼에서 web 사이트 도메인에 정확한
//도메인을 입력해줘야 지도 api 받아올 수 있음
//앱 키는 내 애플리케이션>앱 설정>앱키에서 JavaScript키를 넣어주면 됨

//아래 추가해줘야 빌드할 때 타입스크립트 에러 안 남
declare global {
  interface Window {
    kakao: any;
  }
}

//nextjs에서는 서버 사이드 렌더링때문에 document를 인식 못해서 아래와 같은 조건문 처리 해줌
if(typeof window === 'object') {
    const mapScript = document.createElement("script");

    mapScript.async = true;
    mapScript.src = `//dapi.kakao.com/v2/maps/sdk.js?appkey=0554e7e17897ae59919e5f364fc2abc8&autoload=false`;

    document.head.appendChild(mapScript);

    const onLoadKakaoMap = () => {
      window.kakao.maps.load(() => {
        const mapContainer = document.getElementById("map");
        const mapOption = {
          center: new window.kakao.maps.LatLng(35.99143, 129.21628), // 지도의 중심좌표, (Y, X)값임, x/y가 아님
          level: 3, // 지도의 확대 레벨
        };
        new window.kakao.maps.Map(mapContainer, mapOption);
      });
    };
    mapScript.addEventListener("load", onLoadKakaoMap);
  }

return (
...
<div id="map" style={{width:'90%',height:'300px'}}></div>
...
)
```

### Reference
https://velog.io/@rud285/kakao-지도-kakao.maps.LatLng-is-not-a-constructor
