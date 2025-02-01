# War3-Soulslike-Monster-Data-Analysis

<br><br><br>

## 작업시점

2023년 05월

<br><br><br>


## 소울라이크 몬스터란

![1](https://github.com/user-attachments/assets/2689b18b-7e7c-476e-998d-25e6c83bc17b)

![2](https://github.com/user-attachments/assets/f04be4f8-95e4-436f-9b7f-f2aead697d96)

강한 실시간성,

실시간으로 몬스터의 행동을 보고

실시간으로 유저가 대응해야하는 유형의 몹을 소울라이크 몬스터라 하자

(출처 : 김실장 유튜브)

<br><br><br>


## 분석의 이유와 목표

![3](https://github.com/user-attachments/assets/91ed87e6-265e-44bb-beb5-5ef1bd0a6d7b)

영감은 엘든링 멀기트로부터 받았고,

몬스터의 공격속도가 느리면 오히려 난이도가 올라가는 느낌을 받았는데

실제로 이게 맞는지 정량적인 분석을 해보고 싶었습니다

<br><br>

최종적으로, 

목표는 소울라이크 몬스터의 공격 적중에 대한 분석이 되겠고

​그 외에도 그냥 여러가지 분석 변수들을 추가해봤습니다 

<br><br><br>

## 환경

[![Video Label](http://img.youtube.com/vi/qh8Oc4W31jw/0.jpg)](https://youtu.be/qh8Oc4W31jw)

(이미지를 클릭하시면 플레이 영상이 있는 유튜브 링크로 넘어갑니다)


워크래프트3 유즈맵으로 구현

유저는 몬스터와 대적해서 싸움 <br>

해당 유즈맵을 게임 커뮤니티에 올렸음 <br>
불특정, 다양한 사람들이 이 유즈맵을 플레이하며 데이터를 남김 <br>

<br><br><br>

### 유저

유저 기술은 총 3가지 <br>
공격, 대쉬, 막기 <br>

대쉬 : 거리를 벌릴 수 있음, 0.3초 무적 <br>
막기 : 0.4초 무적 <br>

<br><br><br>

### 몬스터

5개의 공격패턴과 돌진

몬스터는 일련의 과정을 거쳐서 1번의 공격을 시행함

<br><br><br>

### 데이터

![image](https://github.com/user-attachments/assets/efd79efc-1c20-4b7b-be5d-60f768590593)


공격 1번당 데이터 1개를 구성함

공격에 관여하는 여러 변수들과 공격 결과에 대한 정보가 String의 형태로 이어 붙혀져서 서버에 올라감

위 그림과 같이 데이터를 구성해서 서버에 기록

![image](https://github.com/user-attachments/assets/e663cbbb-3073-4820-9541-dfff446c63e0)

위 그림과 같이, 서버에 데이터 로그들이 남겨지며,
해당 로그들을 엑셀 파일에 담아서 데이터 분석에 사용하였음

![image](https://github.com/user-attachments/assets/bccbfd81-fbca-4409-b359-4248b2d1de83)

데이터 1454개

<br><br><br>

## 변수 설명

![image](https://github.com/user-attachments/assets/c929141f-0cbc-467a-b480-02d63fd5023c)

### is_visualization

: 매 공격시 50% 확률로 공격범위를 나타내는 바닥 장판이 보임 <br>
범위 표시를 하게 될 경우 이 값이 true고, 아니면 false임

![1](https://github.com/user-attachments/assets/885826f6-9fa6-4129-8665-6c781faf283f)

<br>

### is_dash

: 멀리 있으면 돌진기 씀 <br>
돌진기를 썼으면 이 값이 true고 아니면 false임

![2](https://github.com/user-attachments/assets/61b5b252-0582-4bf0-aa6c-d179475a3a12)

<br>

### start_distance

: 랜덤 실수값 500~1500 설정했었음 <br>
몬스터 공격시작 탐지 범위, 해당 범위 밖이면 아무 것도 안함 <br>
만약 이 값이 600이고 유저가 700거리에 있으면, 몬스터 아무 행동 안함

<br>

### start_delay

: 랜덤 실수값 0.2~1.0 설정했었음 <br>
유닛 탐지하고나서 본격적인 공격시작까지의 시간

<br>

### pre_delay

: 랜덤 실수값 0.1~0.8 설정했었음 <br>
공격시작 후, 모션을 들어 올리는 시간

![3](https://github.com/user-attachments/assets/251c5806-4458-45c2-b5e7-9f7d684219ce)

<br>

### mid_delay

: 랜덤 실수값 0.1~0.9 설정했었음 <br>
모션 들어 올린 후, 멈추는 시간

![4](https://github.com/user-attachments/assets/217fdfe9-db51-4b90-ba86-5033c74bb334)

<br>

### post_delay

: 랜덤 실수값 0.1~0.7 설정했었음 <br>
공격 모션 후, 최종적인 공격 유효타가 들어가는데 까지 걸리는 시간

![5](https://github.com/user-attachments/assets/78a564c4-1e5f-4c64-b750-20f51771f6ee)

<br>
​

## attack_size

: 랜덤 실수값 175~275 설정했었음 <br>
공격 범위임

### attack_pattern

: 공격 유형임, 1번부터 5번까지 있고 <br>
1 2 3 4 5 번갈아가면서 씀 <br>
1번 5번 패턴은 딜레이가 더 낮고, 대신 공격범위가 좀 더 작음 <br>
2번 3번 4번 패턴은 위에 서술해둔 랜덤 범위값에서 정해짐 <br>

<br>

### attack_count

: 한 유저에게 시행한 공격 횟수 <br>
1부터 카운트 함

<br>

### is_hit

: 유저가 공격에 피격되면 이 값이 true가 됨 <br>
아예 안맞거나 blocked 되면 false임

![6](https://github.com/user-attachments/assets/3f5937c8-6feb-40e7-8237-ae15f7514858)

<br>
​
