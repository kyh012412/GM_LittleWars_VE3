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

### 캐주얼 디펜스 - 패럴랙스를 곁들인 📷카메라 이동 [V18]

#### 사전 준비

카메라 이동에 대한 제어

1. 설정
   1. 캔버스는 pixel perpect라는 기능이 따로 있음
      1. Canvas 컴포넌트 내에서 Pixel Perfect를 체크
   2. Menu Set 비활성화 (작업을 위해)
   3. Game Set 활성화
   4. Bases 활성화
   5. 씬급 변수 Level은 Easy로 설정 후 작업
   6. 카메라 포지션을 x 값을 -2로 설정
      1. 카메라내의 x의 범위는 -2에서 2까지 범위임을 인지
2. Camera Script machine을 만들어줌
   1. 객체급 변수로 Speed (float), isMove(boolean)을 만들어준다.

#### 스크롤 버튼

대상이 모바일 이기에 ui버튼을 넣어서 제어예정

1. Game Set 내에 빈객체 추가(Control Set)
   1. 앵커 최대크기
2. Control Set내에 버튼 추가(Button Right)
   1. 20:30
   2. 앵커 우하단
   3. x -2 y 6
   4. 소스 이미지 Panel
3. Button Right 내의 Text
   1. 폰트 네오둥근모꼴
   2. 라벨 ▶
   3. 폰트 크기 16
   4. 볼드
   5. 색상 38385B
4. Button Right으로돌아와서
   1. event trigger컴포넌트 추가
      1. UI의 여러가지이벤트를 관리하는 컴포넌트
   2. Add event 를하여
      1. point down과 point up을 추가해준다.
      2. 객체에는 카메라를 끌어다가 놓아준다.
      3. 메서드 ScriptMachine.TriggerUnityEvent
      4. 전달 스트링 RightDown 또는 LeftUp 등을조합
5. Button Right를 복사 (Button Left)
   1. pos x -23
   2. 내부 Text방향 반대로
   3. 내부이벤트 String 문자열 변경
6. GameManager graph로 와서
   1. Unity Event 4개 추가
      1. 오타 체크
   2. ![[Pasted image 20240806124822.png]]
7. 테스트
   1. 정상
   2. 테스트중 아래 추가 script 추가

#### 카메라 이동

1. 카메라 그래프 내에서
   1. ![[Pasted image 20240806130758.png]]
   2. ![[Pasted image 20240806130807.png]]
2. 테스트

#### 페럴렉스

1. 카메라는 잘 이동하는 데에 비해 멀리 있는사물이 고정되어 보임
2. 2d에서 원근감을내도록 속도를 달리 해주는 기법
3. script machine을 만들어준다. (Back)
4. Back 1 내부부터 Back 을 넣어준다.
   1. 카메라 이동후 그값을 참조하여 업데이트를 원하기에 late update 사용
   2. Scene 급에 Camera 추가
   3. Object 급에 Offset 이라는 변수 추가 (float)
      1. 상대적인 속도를 반영에 영향을 줄 변수
   4. Back 1(나무)에서 Offset의 값은 0.25
   5. Back
      1. ![[Pasted image 20240806133814.png]]
   6. Back 2에도 붙여넣기 후
      1. offset 0.5
   7. Back 3(Sky)
      1. offset 1
      2. 카메라와 같은 속도로 이동
5. 테스트
   1. 정상

### 캐주얼 디펜스 - 적군,아군 구별하는 유닛 만들기 [V19]

#### 아군 유닛 만들기

1. bs idle을 하이라키 창내로 드랍(BS)
   1. 이름은 BS로 변경
   2. animator 컴포넌트 추가
      1. 컨트롤러는 acbs를 추가해준다.
   3. box collider 2d 추가
      1. is trigger 체크
         1. offset -0.4 1
         2. size 0.6 2
   4. Particles 폴더내에 Dust를 BS 내로 추가
   5. State machine 추가
      1. Class (미정)
      2. Speed float 1
      3. Dust gameObject (자식 객체를 끌어다가 넣어주기)
2. Assets 내에 Scripts 폴더를 만들어주기
   1. MyType.cs
   ```cs
   public class MyType
   {
       public enum Unit {Sword, Range, Guard, Wizard, Bullet};
   }
   ```
3. BS내에 객체급으로 만들어 놓은 Class 의 자료형에 unit m 을 검색하여
   1. Unit of my Type을 선택해준다.

#### 적군 유닛 만들기

1. BS
   1. pos x -1.5
2. BS 복사 (RS)
   1. pos x 1.5
   2. sprite rs idle로 변경(red sword)
   3. Filp X를 체크
   4. animator 내에 controller Acrs로 바꿔준다.
   5. box collider 2d 내에서 offset x의 값을 0.4로 바꿔준다.
   6. state machine의 객체급 변수의 speed를 1대신에 -1로 변경
   7. Rs내의 Dust의
      1. position을 -0.5가아닌 0.5로 변경
      2. rotation y의값을 180
3. Layer를 추가해준다.
   1. 8번에 Blue
   2. 9번에 Red
4. BS에는 Blue layer를 RS는 Red layer를 적용시켜준다.

#### 이동하기

1. 기존에 있는 state이름을 Move로 변경후 그 내부로 이동해준다.
2. 모든 Unit graph가 Object급으로 dust를가진것은 아니므로 null check가 필요하고
   1. null check라는 유닛을 사용한다.
3. par play를 검색하여 유닛을 통하여 파티클 실행
4. ![[Pasted image 20240806183031.png]]
   ![[Pasted image 20240806183150.png]]

#### 적군 감지

1. fixedupdate 물리 효과를 처리하는 생명주기
2. state machine의 trigger unity event 유닛을 넣어준다.
3. 슈퍼유닛 추가 (Macros 내에 SuperUnit 폴더사용)(ScanEnemy)
   1. physics 2d raycast 유닛을 검색
      1. 매개변수가 4개있는 유닛을 선택
   2. 2번째 매개변수에 빔을 쏘는방향을 넣어야 하는데
   3. 빔을 쏘는 대상에 따라 방향이 달라지므로 새로운 script machine을 추가해준다.(TeamValue)
4. TeamValue (script machine) (슈퍼유닛)
   1. trigger input은 없어도 되며
   2. data에 blue (Object / (game object아님))과 red (Object)를 추가해준다.
   3. game object get layer 유닛 추가(layer 값은 int이다.)
   4. output도 trigger없이 반환값만 Object형태로 마늘어준다.
   5. ![[Pasted image 20240806194317.png]]
5. 다시 ScanEnemy로 돌아와서
   1. TeamValue 유닛을 넣어주고 Vector3 right 유닛을 넣어준다.
   2. select on enum을 선택
      1. EnumType을 unit of my type으로 해준다.
   3. Layer와 Layer Mask는 다른것
      1. get mask 검색하여서
      2. layer mask : get mask 유닛을 가져온다.
   4. ![[Pasted image 20240806221329.png]]
   5. raycast hit 2d transform유닛 추가
   6. output trigger는 2개를 주고 Scan과 Null로 해준다.
   7. ![[Pasted image 20240806224419.png]]
6. 다시 BS > Move graph로 이동해준다.
   1. ![[Pasted image 20240806225611.png]]
7. 새로운 script state를 만들어준다.(Attack)
8. transition세팅
9. Attack 내에서 구성
   1. ![[Pasted image 20240806230227.png]]
10. Attack > Move transition 연결해주기

#### 아군 감지

1. ScanEnemy를 복사해준다.(ScanAlly)
   1. ![[Pasted image 20240806230745.png]]
2. Bs > Move 내에서
   1. ![[Pasted image 20240806231700.png]]

### 캐주얼 디펜스 - ⚔️ 근거리 유닛 구현 [V20]

#### 공격 구현

1. BS에 script 변수에 Object 급에 해당하는 변수 선언
   1. HP int 10
   2. ATK int 2
2. BS > Attack 내로이동하여 공격시 atk를 받는대상에게 전달예정
   1. ScanObj에게 damage를 넘기기 위해서 Custom Event 사용
   2. ![[Pasted image 20240807080151.png]]
   3. 이후 Next Action

#### 피격 구현

1. 피격을 구현할 script machine 생성
   1. ![[Pasted image 20240807081936.png]]
   2. ![[Pasted image 20240807081948.png]]
2. BS의 Unit > Move graph로 돌아가서
   1. Hit를 끌어다가 놓아주면 끝이다.
      1. ![[Pasted image 20240807082224.png]]
   2. 이 부분을 Attack,S 내에도 붙여넣기

#### 죽음 상태구현

1. BS graph 내에 Die state 추가
   1. ![[Pasted image 20240807084130.png]]
2. Sprite renderer sorting layer 값 2로 변경
3. ![[Pasted image 20240807084218.png]]
4. 테스트 전
   1. 각 BS 와 RS내에 Object급으로 HP와 ATK가 필요하다.
      1. 그렇지 않으면 에러 발생

#### 방패병 만들기

1. 하이라키에 BS 객체를 BG로 이름 변경
   1. sprite renderer 의 sprite 변경 BG Idle
   2. 런타임 애니메이션 컨트롤러 변경 AcBG
   3. script mahcine 내에 Object급에 해당하는 변수 스펙을 변경해준다.
   4. class Guard로 변경
2. RG도 유사하게 변경
3. 테스트

### 캐주얼 디펜스 - 🏹 원거리 유닛 구현 [V21]

#### 투사체 만들기

1. sprites > Characters 내에 BAA를 하이라키에 드래그
2. 하이라키에 ArrowBlue라는 빈객체생성(ArrowBlue)
   1. 이 객체 이하로 BAA를 옴겨준다.
   2. 옴긴후 BAA의 y축값을 0.3올려준다.
3. ArrowBlue 복사 (ArrowRed)
   1. ArrowRed내의 BAA는 RAA로 교체 (이름 교체, 스프라이트 교체)
   2. RAA의 FlipX 체크
4. Particles 폴더내에 MagicRed와 MagicBlue를 하이라키내로 드래그
5. Layer 설정을 해준다.
   1. 자식객체에도 영향을 주는지에 대한 경고가뜨면 yes를 선택해준다.
6. ArrowBlue에 Bullet이라는 Script machine을 추가해준다.
   1. Object 급으로
      1. Class (unit of my type) bullet
      2. Speed라는 변수 추가 (float) 10
         1. 레드팀의 경우 -10
      3. IsHit (Boolean) false
   2. ArrowRed와 MagicBlue, MagicRed에도 동일하게
      1. script machine과 variables 적용
      2. Magic 계열은 speed를 0으로 수정
         1. 추후 이 값을 통해 arrow와 magic을 구분
   3. 로직
      1. ![[Pasted image 20240807114231.png]]
      2. ![[Pasted image 20240807101706.png]]
      3. ![[Pasted image 20240807114436.png]]
7. Assets 내에 Prefabs 폴더를 만든뒤
   1. Arrow와 Magic을 하나하나 드래그하여서 저장해준다.
      1. Magic을 옴길때 어떤 경고창이 뜨면 original prefab을 골라준다.
8. Base Blue(객체)에 script machine을 추가해준다.
   1. Arrow와 Magic에 각각 prefab을 넣어준다.
9. Base Red에도 유사하게 채워준다.
10. Scene급 변수 추가
    1. Blue에 Blue Base를 Red 에 Red Base를 연결해준다.

#### 원거리 공격 구현

1. 발사를 위한 슈퍼유닛 생성(Shot)
   1. shot의 주체의 layer로 부터 Blue 또는 Red의 string을 가져와서
   2. Base Blue 또는 Red까지 접근하여
   3. input에 있는 name과 조합하여 진영에맞는 Arrow 또는 Magic을 생성
   4. shot의 주체의 공격력을 가져와서 생성된 객체에 동일한 값 넣어주기까지
   5. instanticate중 original position rotation의 값을 가지는 것을 선택
   6. ![[Pasted image 20240807105121.png]]
2. Unit graph로 돌아와서
   1. Switch on Enum을 사용하여 분기처리
   2. Attck state내에서
      1. ![[Pasted image 20240807111051.png]]
      2. ![[Pasted image 20240807111101.png]]
      3. ![[Pasted image 20240807111111.png]]

#### 궁수와 법사 만들기

1. BA와 RA 만들어주기
   1. 이름
   2. sprite
   3. ac 변경
   4. class r
   5. hp 5
   6. ATK1
   7. speed 1
2. BW와 RW만들어주기
   1. Blue 기준
   2. -5.8,1.4
   3. order in layer -1
   4. 애니메이터
   5. class w
   6. hp1
   7. speed 0
   8. atk 1
   9. 마법사 객체 이하의 dust는 삭제
3. 테스트
   1. BABW RARW를한개씩만 남기고 나머지를 지운후 테스트

### 캐주얼 디펜스 - 유닛 구매기능 구현 [V22]

#### 블루팀 프리펩

1. BW를 복사해준다. (BWU)
   1. 이름
   2. 스프라이트
   3. ac
   4. atk 2
2. BAU
   1. hp 8
   2. atk2
   3. speed 1.5
3. BGU
   1. hp 45
4. BSU
   1. hp 15
   2. atk3
   3. speed 2
5. prefab화 시키기전에
   1. 법사를 제외한 나머지들은 x위치를 -5로 맞춰주기
   2. Assets/Prefabs/Unit 폴더를 만들어주고 하나하나 옴겨준다.(프레펩화)
6. 하이라키상에는 법사만 남기고 삭제
   1. 법사들은 Base Blue 이하로 옴겨준다.
   2. 그리고 비활성화 해준다.
7. 각각마다 Dust가 잘 연결 되어있는지 확인한다.

#### 레드팀 프리펩

1. 로직 상 동일

#### 유닛 UI 기틀잡기

1. Control Set 이하에 빈객체 추가(Blue)
   1. 앵커 좌하단
   2. 가로 150 세로 70
   3. grid layout group이라는 컴포넌트 추가
      1. Cell Size : 칸하나가 찾이하는 크기
         1. 30,30
      2. Spacing 칸과 칸사이의 공간
         1. 1,10
      3. Start Axis (횡방향 또는 종방향으로 채울 방향)
         1. Vertical (종방향 먼저 채우고 횡방향으로 1칸)
      4. Child Ailgnment
         1. lower left
2. Blue이하에 button 추가(Btn BW)
   1. 이미지 소스 Panel
   2. 이하텍스트삭제
3. Btn BW이하에 이미지 추가(Portrait WZ)
   1. 이미지 소스 Portrait WZ
   2. set native size
   3. 앵커 상단
4. Btn BW에 script machine 추가(BtnUnit)
   1. Object급에 변수추가
      1. Level int 0
      2. IsWizard boolean false
      3. Unit aot list
         1. - 두번
         2. Game Object BW (를 prefab에서 끌어서 넣어준다.)
         3. Game Object BWU(업그레이드가 인덱스 뒷쪽의 번호로)
5. Btn BW에 button 컴포넌트에서 On Click 이벤트를 추가
   1. 객체 자기자신 Button
   2. 메서드 scriptmachine.triggerunityevent
   3. Buy
6. Blue (객체)에서 빈 객체 추가(Btn BWU)
   1. Blue 내에서 순서를 Btn U먼저 그후 Button이 되게 바꿔준다.
7. Btn BWU내에서 Button 추가(Btn U)
   1. 앵커 아래쪽이 꽉차게
   2. 높이 12
   3. 좌우 3,3
   4. 소스 이미지 panel
   5. 이하의 텍스트 삭제
   6. On Click에 아까만든 Btn BW을 연결
      1. 객체 Btn BW
      2. scriptmachine.triggerunityevent
      3. Up
8. Btn U내에 Image를 추가해준다.(Upgrade Image)
   1. 소스 이미지 icon upgrade
   2. set native size
   3. pos y 3
9. BW에 대한 한쌍의 버튼이 완성됨
   1. ![[Pasted image 20240807201815.png]]

#### 유닛 종류별 UI

1. ![[Pasted image 20240807201915.png]]
2. 추가로 만들어준 후 작업시작
   1. BW, BA, BS, BG
   2. ![[Pasted image 20240807202343.png]]
   3. 위와 같이 바꿔주며 아래작업을 병행
3. Btn BA의 내부에 Unit 에있는 2개의 오브젝트 변경
   1. ![[Pasted image 20240807202107.png]]
4. Btn BAU 내의 Onclick에 연결된 객체가 Btn BA인것을 확인 할 수 있다.
5. Btn BA 이하의 Image 소스변경 Portrait A
6. Btn BS 이하의 Image 소스변경 Portrait S
7. Btn BG 이하의 Image 소스변경 Portrait G
8. Btn BW의 Button 컴포넌트 비활성화
   1. IsWizard boolean값 true
   2. Unit에 있는 객체들을 prefabs이 아닌 Base Blue이하의 것들로 바꿔준다.
   3. 대상을 눌렀을때 이런식으로
      1. ![[Pasted image 20240807202958.png]]
      2. 활성화가 되어야한다.
   4. Unit 리스트에 0번째에 인덱스를 추가해주고 Game Object에 None인것으로 넣어준다.
      1. ![[Pasted image 20240807203130.png]]
9. Blue 객체를 복사해준다. (Red)
   1. 앵커 우상단
   2. grid layout group 컴포넌트내에
      1. Child Alignment 값을 Upper Right로 해준다.
   3. Red 이하의 객체들의 이름을 전부 바꿔준다.
   4. RW내에 Object에 잇는 변수값 바꿔주기
   5. RA,RS,RG 내에 Object 값 바꿔주기
10. Btn BW에 잇는 BtnUnit graph에서 작업

#### 유닛 생산 구현

1. Btn BW에 잇는 BtnUnit graph에서 작업
   1. ![[Pasted image 20240807210305.png]]
   2. ![[Pasted image 20240807210313.png]]
   3. ![[Pasted image 20240807210322.png]]
2. 테스트
   1. 법사를 3번업그레이드하면 에러발생 (예외 처리 필요)
3. 후처리
   1. Red 팀의 앵커를 우하단에 배치한 후에

### 캐주얼 디펜스 - 실제 게임같은 💰자원 시스템 구현 [V23]

#### 자원 시스템

자원 개념 추가 예정

1. 자원 시스템
2. Base Blue에 Object급으로 변수 추가
   1. Cost (int) 0
   2. layer 변경
3. Base Red도 동일
   1. Cost (int) 0
   2. layer 변경
4. 매크로 폴더 내에 script machine 추가(Base)
5. 독립적인 흐름을 위해 Start를 coroutine으로 설정
6. wait for seconds 유닛을 추가
7. ![[Pasted image 20240808081144.png]]

#### 자원 바 UI

1. Control Set > Blue 의 위치변경
   1. pos x 6 pos y 9
2. Control Set이하에 Image 추가 (Cost)
   1. pos x 2 pos y 2
   2. 150 : 10
   3. 순서 조정
      1. ![[Pasted image 20240808081536.png]]
   4. 소스 이미지 bar back
   5. layer blue
3. Cost 내에 Image 추가(Bar)
   1. 앵커 왼쪽부터 상하 꽉채우기
   2. 가로 150
   3. 소스 bar front
   4. color f5bf63
4. Cost내에 Text 추가(Cost Text)
   1. 앵커 우상단
   2. 가로 세로 0 0
   3. 중앙정렬, 중앙정렬
   4. overflow,overflow
   5. 라벨 00
   6. pos x -10 y -2
   7. 네오 둥근모꼴
   8. 볼드
   9. 폰트크기 12
5. Cost Text 복사 (Cost Shadow Text)
   1. Cost Shadow Text는 Cost Text보다 위쪽에 배치시킨다.(하이라키기준)
   2. pos y -2.5
   3. 362a23

#### 자원 로직 연결

1. Script machine 생성 (TeamBase)(슈퍼유닛)
   1. 외부에서 문자열을 받고
   2. 현재 layer에따라 Base로부터 해당하는 오브젝트를 뽑아준다.
   3. 만약에 문자열이 비면 해당하는 Base를 받는다.
   4. ![[Pasted image 20240808083914.png]]
2. Script machine 생성 (Bar)(Macro)
   1. Cost > Bar 객체에 graph로 넣어주기
   2. Object급 변수 추가
      1. Var String Cost
      2. Max int 10
      3. Text / Text / Cost Text
      4. Text Shadow / Text / Cost Shadow Text
   3. Start 유닛 부터 시작
   4. rect transform get size delta
      1. 실제 UI크기를 가지고 있는 변수
      2. 여기서 x,y가 폭과 높이가 됨
   5. ![[Pasted image 20240808085030.png]]
   6. ![[Pasted image 20240808090618.png]]
   7. ![[Pasted image 20240808091030.png]]

#### 구매 로직

1. Control Set > Blue ,Red 의 layer를 UI가 아닌 각각 Blue,Red로 변경
   1. children도 같이 바꾸기 에 yes
2. 각 항목에 Cost 추가
   1. Btn BW에 Cost 추가 int 0
   2. Btn BA에 Cost 추가 int 5
   3. Btn BS에 Cost 추가 int 3
   4. Btn BG에 Cost 추가 int 7
   5. Red 쪽도 동일
3. 슈퍼 유닛 생성(Buy)
   1. input output 추가
   2. Check Cost
   3. ![[Pasted image 20240808095525.png]]
4. 다시 (Btn BW)BtnUnit으로 와서 Buy 그룹 수정
   1. ![[Pasted image 20240808095829.png]]
   2. ![[Pasted image 20240808101301.png]]
   3. Late update 추가 예정
   4. Select Unit
      1. 참거짓에 따라 어떤 값을 선 가공
   5. 각 객체마다 Object 급 변수추가
      1. Btn U / Game Object / Btn \~\~U 내의 Btn U
5. Cost > Bar 의 Layer를 Blue로 변경
6. 테스트 / 정상

#### 유닛 UI 구체화

1. Control Set > Blue
   1. pos x 6 pos y 9
2. blue > Btn Bs > Image
   1. pos y 12
3. blue > Btn BS에 이미지 추가(HP)
   1. 소스 icon hp
   2. set native size
   3. 앵커 아래
   4. pos x -6 y 6
4. HP > Text 추가 (HP Text)
   1. 가로세로 0 0
   2. 라벨 0
   3. 둥근모꼴
   4. 폰트크기 7
   5. 중앙정렬, 중앙정렬
   6. overflow overflow
   7. 색상 하얀색
   8. pos x 0.2
5. HP 복사 (ATK)
   1. pos x 6
   2. 소스 icon atk
6. ATK 복사 (Cost)
   1. 소스 icon cost
   2. pos x 0 y -4
7. Cost > Text
   1. 색상 b93600
   2. pos y -0.5
8. Btn Bs > Image(Portrait)에 script machine 추가 (embed)
   1. Btn Bs(현재는) 를 graph내로 드래그해서 넣어준다. (새로운 유닛 생성됨)
      1. 이것이 가능한 이유는 embed 타입이기 때문이다.
      2. 매크로 타입은 불가능
   2. ![[Pasted image 20240808111510.png]]
9. 이 전체를 복사하여서 HP > Text에서도 사용 script machine embed
   1. ![[Pasted image 20240808111933.png]]
10. 전체를 복사하여 ATK > Text에서도 사용 embed
    1. HP 부분만 ATK로 수정
11. Cost > Text
    1. ![[Pasted image 20240808112224.png]]
12. Btn BA와 Btn BG,Btn BW에 대해서도
    1. portrait hp,atk,cost에 관한 text 총 각각 4개씩 바꿔줘야한다.
       1. portrait부터 각각 옴겨주고
          1. BW의 경우에는 다음처럼 구성
             1. ![[Pasted image 20240808112857.png]]
       2. hp,atk,cost는 ctrl D로 복사후
       3. 타객체로 이동후
       4. pos 값을 조정하는 쪽이 편하다.
       5. 각각의 객체내의 Text 내의 script graph가 참조하는 값들을 변경해준다.
    2. Btn BW는 ATK만 있으면된다.
       1. 내부로직도 null check가 필요하다.
       2. ![[Pasted image 20240808113953.png]]
13. 테스트

###
