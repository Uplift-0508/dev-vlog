# 플랫폼 API

리액트 네이티브는 스마트폰의 카메라롤, 위치, 영속되는 저장소 등을 쉽게 사용할 수 있게 해줍니다. 플랫폼 특유의 API 는 리액트 네이티브에 내장된 모듈을 통해 사용하기 편리한 비동기 자바스크립트 인터페이스로 제공됩니다. 물론 플랫폼의 모든 기능을 제공하지 않기 때문에 일부 API 들은 직접 모듈을 만들어서 써야 하거나 리액트 네이티브 커뮤니티에서 다른 사람이 만든 모듈을 사용해야 합니다. 

## 지리적 위치 정보 이용하기
리액트 네이티브는 지리적 위치 추적 (geolocation) 기능을 기본적으로 제공합니다. 이 기능은 플랫폼에 상관없이 동일하게 사용할 수 있습니다. 이 기능은 MDN Geolocation API 웹 명세서를 따르는 형식의 데이터를 리턴합니다. 명세서의 내용을 준수하고 있기 때문에 위치 서비스와 같은 플랫폼 특유의 API 를 직접 다룰 필요가 없고, 위치를 다루는 코드가 모든 플랫폼에서 동일하게 동작합니다. 

```
navigator.geolocation.getCurrentPosition(  
    (position) => {  
        console.log(position);  
    },  
    (error) => {  
        alert(error.message)  
    },  
    {enableHighAccuracy: true, timeout: 20000, maximumAge: 1000}  
);
```

### 권한 다루기
위치 정보는 민감한 개인정보이기 때문에 기본적으로 앱이 바로 접근할 수 없습니다. 이런 정보에 대한 접근은 허용되거나 거절당할 수 있기 때문에 모든 경우를 대비한 코드 작성이 필요합니다. 
iOS 의 경우, NSLocationWhenInUseUsageDescription 항목을 리액트 네이티브 앱 생성 시 기본으로 포함되는 Info.plist 파일에 추가해야 합니다. 


AndroidManifest.xml
```
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbODkzMTczMDA0LDE4MjM3NTA5OTUsMTIzMD
c2OTgxMCwxMjIxOTc0ODM0XX0=
-->