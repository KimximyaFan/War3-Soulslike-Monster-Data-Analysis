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

<br><br>

![image](https://github.com/user-attachments/assets/e663cbbb-3073-4820-9541-dfff446c63e0)

위 그림과 같이, 서버에 데이터 로그들이 남겨지며,
해당 로그들을 엑셀 파일에 담아서 데이터 분석에 사용하였음

<br><br>

![image](https://github.com/user-attachments/assets/bccbfd81-fbca-4409-b359-4248b2d1de83)

데이터 1454개

<br><br><br>

## 변수 설명

<br>

![image](https://github.com/user-attachments/assets/c929141f-0cbc-467a-b480-02d63fd5023c)

<br><br><br>

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
### attack_size

: 랜덤 실수값 175~275 설정했었음 <br>
공격 범위임

<br>

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

<br><br><br>
​
## is_visualization 변수에 대한 분석

![image](https://github.com/user-attachments/assets/d5f672c0-f4c0-4f10-ba12-b74fcf0d2d80)

왼쪽은 바닥 패턴을 보여줬을 때, 오른쪽은 안보여줬을 때 <br>

히스토그램으로 보면 차이가 조금 있어 보이는데,
수치적으로 보면 2.5% 밖에 차이가 안납니다

바닥 패턴 보여주면 맞을 확률이 51.09% <br>
안보여주면 맞을 확률이 53.61%

생각보다 그렇게 큰 차이가 안나는 것으로 보아 <br>
바닥 패턴 보여주는게 유저에게 도움이 되는지, <br>
실효성있게 난이도를 낮춰주는지 의문이 드는 결과 <br>

한 유저의 의견으로는, <br>
바닥 패턴보다는 몬스터의 모션에 집중했다고 하였음

<br><br><br>
​
## is_dash 변수에 대한 분석

![image](https://github.com/user-attachments/assets/1f701c40-499c-4b83-bdb9-02c5eac0f1cc)

왼쪽은 돌진을 안썼을 때, 오른쪽은 돌진을 썼을 때 <br>

몬스터의 돌진이란 행동이 유저에게 어떻게 다가올지, <br>
압박감의 형태로 작용해서 유의미한 차이를 낼 것인지 궁금했습니다

돌진을 쓰면 맞을 확률이 5% 정도 증가하긴 하는데, <br>
막 그렇게 드라마틱한 차이는 아닌 걸로 보입니다<br>

그리고 기본적으로 돌진은, 몬스터와 유닛과의 거리가 멀 때 사용하는 것이라<br>
거리가 멀다 = 컨트롤에 자신이 없다 = 미숙하다 <br>
이런 요인도 생각해볼 수 있기 때문에 <br>
유의미한 효과는 더 줄어든다고 봐야하나 싶긴 합니다 <br>

<br><br><br>

## start_distance 변수에 대한 분석

![image](https://github.com/user-attachments/assets/49c856bb-5210-4a1a-86c0-c4ec17d85599)

범위를 100 단위로 그룹화 한뒤, 해당 그룹에서 is_hit 변수의 1의 갯수랑 0의 갯수를 

히스토그램으로 그려본 그래프입니다

해당 막대 크기에서 1의 비율이 적중률을 의미하고

앞으로 이런 그래프를 계속 그릴 예정입니다


![image](https://github.com/user-attachments/assets/3604eca0-c39b-473d-bb3b-03cff35bde8b)

적중률 그래프를 그리고

적중률에 대해서 linear regression을 적용했습니다

탐지 범위가 높을 수록 적중률이 증가하는 추세? 

라고 말할 수 있겠습니다만

​![image](https://github.com/user-attachments/assets/fd571adb-5c4c-4e1d-9d00-424826cc4cd9)

탐지 범위를 50 단위로 세분화 해봤더니 1350~1500 범위에서 기울기를 견인해버림을 알 수 있습니다

1350 까지 커팅하고 다시 적용해보면 

파란선을 보다시피 감소하는 추세인데

그러면 탐지 범위가 높을 수록 적중률이 감소하는가? 

이라고 말할 수도 없습니다

​

데이터 수집 환경 자체가, 돌진 때문에 1000이상 거리 벌리기가 쉽지 않습니다

그래서 딱히 유의미한 데이터가 되진 못하는 것 같습니다

<br><br><br>

## start_delay 변수에 대한 분석

![image](https://github.com/user-attachments/assets/47e1c4c6-ed1d-45b7-a596-ef4279055b94

start_delay는 유닛은 탐지후 공격 시작까지의 시간입니다

적중률 그래프를 보면

유의미하게 감소하는 추세임을 직관적으로 알 수 있습니다

이게 유저가 막기가 아닌 대쉬로 도망 갈 수 있기 때문에

대응 시간이 길수록 맞을 확률이 유의미하게 줄어드는 것 같습니다

<br><br><br>​

## attack_size 변수에 대한 분석

![image](https://github.com/user-attachments/assets/18ee062d-53bb-447e-a5b0-32630eac19e4)

당연하게도

공격사이즈 커질수록 당연히 맞을 확률이 올라가겠습니다

230부터 데이터 량이 적은 이유가, 1번 5번 공격패턴은 공격 사이즈가 더 낮아서 그렇습니다

![image](https://github.com/user-attachments/assets/f7e0a77e-4320-4727-9431-a8252c39396c)

데이터량이 많은 220까지만 커팅하고 5단위로 그룹화해서 다시 그래프 그려보면

추세가 더 직관적으로 나타납니다

<br><br><br>
​
## attack_pattern 변수에 대한 분석

![image](https://github.com/user-attachments/assets/23e9ed00-861b-4990-a539-65a8d96ad559)

1번 5번 패턴은 딜레이가 낮은 대신 공격 범위가 작다고 했는데요

1, 5 와 2, 3, 4 적중률 차이를 보면 

공격 범위 보다는 

공격 딜레이가 적중률에 영향을 끼침을 간접적으로 알 수 있습니다

<br><br><br>

​## attack_count 변수에 대한 분석

![image](https://github.com/user-attachments/assets/0e2e3885-84ec-441b-b873-433b78562831)

직관하고 반대되는 결과가 나왔습니다

attack count가 늘어갈 수록 사람들이 적응하고 학습해서 적중률이 점점 낮아지는 추이가 나올 줄 알았는데

그 반대로 나왔습니다

count 값 15 이후로는 데이터량이 적어서 유의미한 분석이 아니라 치고 커팅한다해도

추세 자체는 변하진 않을거 같습니다

![image](https://github.com/user-attachments/assets/9a18b15f-d432-420f-b729-a0b526fbfc5a)

평균적으로 6회 정도 되니 

6까지만 커팅

![image](https://github.com/user-attachments/assets/89b761cf-b6e6-48cb-a068-aa5a3f586d71)

그래도 증가하는 추세고, 어디서 커팅하든 비슷할거 같습니다

어택카운트가 높아져간다 -> 전투가 길어진다 -> 유저가 못하기 때문에 전투가 길어진다 -> 못하니 피격확률이 높다

이런 추론도 가능할 것 같습니다

## pre_delay, mid_delay, post_delay 변수에 대한 분석

일단 이 세변수 분석이 제일 하이라이트고

pre + mid + post 를 다 더하면 전체 공격 딜레이를 의미합니다

그래서 저 세 변수를 더해서 새로운 변수를 만들어서 분석해보는 것이 굉장히 의미가 있어 보이고

이를 total_delay라 명명 했습니다

![image](https://github.com/user-attachments/assets/6814aa14-7a91-466a-b6a5-67e62f2c2a50)

일단 pre_delay, mid_delay, post_delay를 봅니다

​![image](https://github.com/user-attachments/assets/4434ffe6-528e-4ce0-9c6e-26ef22f817f9)

re_delay를 0.1 단위로 그룹화 해서 적중률 분석

Linear regression 적용해보면 감소하는 추세는 맞으나

1차 polynomial regression은 자극히 interpretability에 집중한 분석이니

2차 poly fit도 적용을 해봅시다
​
![image](https://github.com/user-attachments/assets/2d327450-9f5e-48ce-894b-890331a98e41)

뭔가 꺾이려는 기세가 있습니다

이런 경향은 pre 뿐만 아니라 mid, post 에도 동일하게 나옵니다

![image](https://github.com/user-attachments/assets/d944f5fa-1cfc-475f-b1cb-40f9995cd248)

mid, post 둘다 linear regression적용 해봤으나, 

확실히 2차 poly fit이

데이터를 더 잘표현한다는 느낌을 다음 그림들을 통해 받을 수 있습니다

![image](https://github.com/user-attachments/assets/65d52e7e-ce45-445f-be61-ed47c9942663)

mid 딜레이는 확실히 꺾이는 경향이 직관적으로 보입니다

![image](https://github.com/user-attachments/assets/8dba8398-54f3-47a2-8e8c-a5433c09195c)

post 역시 그렇습니다

이제 새롭게 만든 데이터인 total_delay를 분석해봅시다

![image](https://github.com/user-attachments/assets/c8a7e620-ec3d-4f85-8b64-347d7857f117)

일단 커팅이 필요한 구간들이 몇개 보입니다

0.3~0.4 그리고 2.0 이후로는 데이터가 너무 적어서 유의미한 분석이 안될 것 같으니 잘라냅시다

![image](https://github.com/user-attachments/assets/053aa13d-b399-438c-8e1f-9afd376570b8)

커팅후 linear regression 적용

단순하게 interpret 하려면 감소하는 추세다! 라고 말할 수 있겠으나

![image](https://github.com/user-attachments/assets/382d3525-6df1-4d57-a5fc-2da95a785ba8)

다음 그래프 피팅이 좀 더 데이터를 잘 표현하는 것 같습니다

그리고 확실히, 딜레이가 오히려 높을 때, 피격확률이 높아지는 구간이 존재합니다

그 기준이 1.1초입니다

공격 딜레이 1.1초를 기준으로 오히려 적중률이 증가하는 경향성을 보입니다

물론 빠르게 때릴지 느리게 때릴지 모른다는 전제가 깔려 있어야하겠습니다

그 후 1.7초 이후로 다시 감소하는데, 이는 유저가 대쉬를 통해서도 공격을 피할 수 있기 때문에

이제 확실한 대응시간이 주어져서 맞을 가능성이 낮아지기 때문으로 보입니다

이 분석을 통해 

소울라이크 몬스터의 공격속도가 느리면 

특정 구간에서 오히려 쳐맞을 확률이 높아짐을 지표를 통해 알 수 있게되었습니다

![1](https://github.com/user-attachments/assets/9669f5f8-f992-4f0a-81e5-f1d4ec3a2fda)

해당 내용을 기반으로 몬스터의 공격 딜레이를

1.8초라는 구체적인 값으로 패턴을 정해놨었고

왜 적중률이 높은지 보여주는 대표적인 gif 입니다

## 상관성 분석

![image](https://github.com/user-attachments/assets/aa0a2441-b84a-44e2-a973-5b72c9882e00)

![image](https://github.com/user-attachments/assets/90a77bf0-5701-4fd7-94c9-a633ba69a840)

그냥 나이브하게 

is_hit 의 0 1 밸류에 대한 상관성 분석을 해봤습니다

post_delay가 영향력이 크고

total_delay가 2등인 것으로 보아, 변수 합쳐서 total_delay 만들어서 분석한건 유의미함을 알 수 있습니다

pre_delay는 순위에 없어서 막 크게 유의미한 지표가 아닌가보네요

## 결론

소울라이크 몬스터일 때, 

공격속도가 낮으면 오히려 적중률이 증가한다

그 기준은 1.1초

1.1초 이후로 증가하다가 1.7~1.8초 즈음에 다시 감소함

해당 분석은 몬스터 제작 난이도 설계에 유용하게 사용될 수 있다

공격속도가 빨라서 피격되면 불합리 하지만

공격속도가 느린데 맞으면 합리적인 난이도 설계이기 때문




