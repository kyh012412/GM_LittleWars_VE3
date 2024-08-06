https://www.youtube.com/watch?v=IONpYgEfk40&list=PLO-mt5Iu5TebYBC5jE3u5LyP2D7np0jJf

### 캐주얼 디펜스 - 메인메뉴 만들기 [V17 + Asset]

#### 에셋 다운로드

1. [에셋 링크](https://assetstore.unity.com/packages/2d/characters/bolt-2d-littlewars-assets-pack-189896)

#### 배경 배치

1. 배경세팅 3. sprites 내에 background에 4가지 이미지가 있음 1. 각각을 하이라키창내로 드래그 4. 빈객체 만들어주고(Back Group) 1. 위치초기화 5. Back 0 만 y 값을 -3 6. ~~순서는 위 순서대로 여야 한다.~~ 1. ![[Pasted image 20240806090345.png]] 7. Back 3의 Order in layer 값 -10 8. back 2의 값 -9 9. back 1의 값 -8 10. back 0의 값 -7
2. Base 세팅
   1. Base blue와 Base Red를 한 개씩 넣어준다.
      1. blue x -6 red x 6

#### 카메라 해상도 설정

1. game tab에서 가로 세율 비율이 19:9로 맞춰준다.
2. 카메라에 pixel perpect camera 컴포넌트를 추가해준다.
   1. 별도의 설치는 불필요 (버전차이)
   2. Assets Pixels Per Unit 20
   3. 190 : 90의 비율로 만든후
   4. run in edit mode를 클릭(토글방식이므로 잘봐야한다.)
3. UI Canvas 오브젝트 추가
   1. Canvas Scaler
      1. UI Scale Mode 의 속성값 Scale With Screen Size
      2. 285:135로 설정
      3. Pixel per unit 20

#### 메뉴화면 만들기

1. 캔버스 내에 빈 오브젝트 추가(Menu Set)
   1. 앵커 최대 크기
   2. image 컴포넌트 추가
   3. 색상 검은색 알파 100
2. Menu Set내에 빈 객체 추가 (Title Set)
   1. 이미지 객체 추가(Image)
   2. pos y 20
3. Image 내에서
   1. 이미지소스 titles 에 있는 littewars를넣어주고
   2. set native size
   3. scale 2,2,1을 준다.
4. Image를 복사한다. (Image Shadow)
   1. Color black 알파 100
   2. pos y -5
5. Menu Set 내에 Button UI 생성
   1. 소스 이미지 panel
   2. pos y -30
   3. 40:25
6. Menu Set > Button > Text
   1. 의 폰트를 네오둥근 모꼴로 변경 (상용으로 사용 가능한 오픈폰트)
   2. 폰트 크기 9
   3. 라벨 보통
   4. 텍스트 컬러 흰색
   5. bottom 6
7. Text 복사(Sub Text)
   1. bottom 0 top 8
   2. 라벨 Normal
   3. 폰트크기 6
   4. 색상 607591
8. Button 이하에 Image 객체추가
   1. 소스 이미지 icon clear
   2. set native size
   3. 앵커 좌상단
   4. pos x -1 y 6
   5. 이미지 (객체가아닌) 컴포넌트 비활성화
9. Button을 복사 ()
   1. pos x -50
   2. 내부 text 라벨 쉬움
   3. 내부 sub text라벨 easy
10. Button을 한개 더 복사
    1. pos x 50
    2. 어려움 / Hard
11. 각버튼에 네이밍
    1. Button Easy Normal Hard
12. Canvas 내에 새로운빈객체 추가 (Game Set)
    1. 앵커 최대 크기확장
    2. 나중에 구현 예정

#### ~~볼트설치~~

1. 버전차이로 설치불필요

#### 볼트 손풀기

1. Saved급에 IsClearEasy (boolean)변수를 만들어줌
   1. 난이도별로 하나씩 만들어주기
2. VisualScripting SceneVariables 와Event System은 지우지않고 camera 이하의요소로 넣어주기
3. Canvas > Menu Set > Button Easy > Image에 script machine추가 (Embed)
   1. ![[Pasted image 20240806102823.png]]
   2. copy component 후에 다른 Image로 가서 Paste Component as new
   3. Saved에서 가져오는 변수만 올바르게 맞춰준다.
4. 순수 코드로 title을 상하로 움직이는 로직구현해보기 ( animation없이)
   1. Title Set으로가서 add component 스크립트 머신추가
   2. Asset 내에 Macros 폴더를 만들어주고 매크로를 만들어주기
   3. Graph 단위에 Frame(float) 변수를 만들어주기
   4. ![[Pasted image 20240806104838.png]]
5. Button Easy에 script machine 추가 (embed)
   1. Event > GUI > On Button Click 이벤트 유닛 추가
   2. Scene급 변수에 Level 이라는 변수추가 (String)
   3. Base Blue Red 둘다 비 활성화 (객체급에서)
   4. ![[Pasted image 20240806111118.png]]
6. 위 코드를 Normal 과 Hard에도재사용 (String 매개변수 값만 변경)
7. 테스트

   1. 씬급 변수에 올바른 값이 들어가는 지 확인
   2.

###
