# flutter unity widget 사용법

## 우선 flutter 파일 안의 unity 파일을 만든 후 파일안에 unity 파일 생성

## unity에서 먼저하는게 편한거 같긴함

## unity

1. Assets -> Import Package -> Custom Package
   - Flutter_Unity_Widget 패키지
2. File -> Build Settings

   - Mono -> ll2CPP
   - 최소 API (28), 최대 API 설정 (32보다 크게)
   - ARM64, ARMv7

3. Export

4. Edit -> Preferences -> NDK경로 복사 -> flutter에 붙여넣기

- 할 때 \\ 두개 할 것!
  C:\Program Files\Unity\Hub\Editor\2022.3.9f1\Editor\Data\PlaybackEngines\AndroidPlayer\NDK

## flutter

1. pubspec.yaml에다가

   dependencies:
   flutter_unity_widget: ^2022.2.0

2. android안의 local.properties에다가

   - ndk.dir=C:\\Program Files\\Unity\\Hub\\Editor\\2022.3.9f1\\Editor\\Data\\PlaybackEngines\\AndroidPlayer\\NDK

3. android/app/build.gradle에다가

   - android 안의 defaultConfig 안에

   - minSdkVersion - 유니티에서 설정한 최소 API (32)
   - targetSdkVersion - 유니테에서 설정한 최대 API (34)

   - ex
     minSdkVersion 32
     targetSdkVersion 34

   - android 안에 ndkVersion = "21.3.6528147"
     - 이거는 크게 ndk버전 호환이 안될경우

4. unityLibrary 파일의 build.gradle안의

   - 실행 하다보면 여기서 libmain.so.exe 오류가 발생할 수 있다.
   - 일단 flutter clean으로 정리하고, flutter pub get으로 업데이트 한 후 기다렸다가 실행 해보기
   - 그래도 안되면 일단 껐다가 킨 후 설정 다 되면 실행 하기

5. 이제 아래 코드를 main.dart에 넣기

- import 'package:flutter/material.dart';
  import 'package:flutter_unity_widget/flutter_unity_widget.dart';

void main() {
runApp(MyApp());
}

class MyApp extends StatelessWidget {
@override
Widget build(BuildContext context) {
return MaterialApp(
title: 'Flutter Unity Integration',
theme: ThemeData(
primarySwatch: Colors.blue,
),
home: UnityScene(),
);
}
}

class UnityScene extends StatelessWidget {
@override
Widget build(BuildContext context) {
return Scaffold(
appBar: AppBar(
title: Text("Unity Scene"),
),
body: UnityWidget(
onUnityCreated: (controller) {
// Unity 초기화 코드를 추가하려면 이 곳에 작성합니다.
},
),
);
}
}
