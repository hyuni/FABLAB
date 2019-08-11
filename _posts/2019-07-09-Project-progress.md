---
title: "Project Progress"
categories:
  - FABLAB
tags:
  - Project
  - Fusion 360
  - Drone Frame
---


### Drone Frame 모델링

1. 아두이노 Mega ADK 보드

   |항목 | 제원|
   |:-- | --:|
	|Length| 101.52 mm|
	|Width	| 53.3 mm|
	|높이(Thickness) | 알수없음(약 22mm)|

2. 밧데리(TW503048)

   |항목 | 제원|
   |:-- | --:|
	|Length| 48 mm|
	|Width	| 30 mm|
	|높이(Thickness) | 5mm|

3. 	모터 및 프로펠러

	* 프로펠러

   |항목 | 제원|
   |:-- | --:|
	|Length| 75 mm|
	|샤프트 길이	| 7.8 mm|


	* 모터

	|항목 | 제원|
   |:-- | --:|
	|Length| 16 mm|
	|지름	| 7 mm|

4. 모델링된 이미지

	![Screenshot - Drone frame](https://github.com/hyuni/FABLAB/raw/master/download/Project/Drone_frame_v4.png)


## Drone S/W

### Arduino

### Drone Controller Android App

1. [HexAirbot 의 HexNanoController_Android](https://github.com/HexAirbot/HexNanoController_Android) 기반으로 SkyRover 프로젝트에서 사용 했으나 그동안 수정된 부분이 반영되어 있지 않음.

2. 따라서 [HexAirbot 의 HexNanoController_Android](https://github.com/HexAirbot/HexNanoController_Android) 기반에서 프로젝트를 fork 후 관련된 코드를 수정해야 함.



### Reference site 정리

1. [HexAirbot 의 HexNanoController_Android](https://github.com/HexAirbot/HexNanoController_Android)
   - 2014/8/11 일자의 commit 이 삭제된것으로 보여지며, 그 다음 커밋이 2014/8/15 임.

2. [exxamalte 의 HexNanoController_Android](https://github.com/exxamalte/HexNanoController_Android)
   - bluetooth connection 기능 추가
   - base 프로젝트가 HexAirbot 의 HexNanoController_Android 이며, git commit iD 가 ed0fb6744a117930f31ca9c69540c214ac4d3e81 (2014/8/11)
