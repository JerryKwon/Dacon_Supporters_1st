# 데이콘 서포터즈 1기

## :calendar: 진행일정
2020년 3월 16일(월) ~ 2020년 4월 말

	* 1주차: 대회에 대한 이해, 탐색적 데이터 분석
		* 진행: 스터디 팀장님 (2명 - 대회에 대한 이해 1명, 탐색적 데이터 분석 1명)
		* 숙제: (스터디원 수준에 따라) BaseLine code Beginner or Itermediate clone coding
	* 2주차: Feature Engineering, 분석모델 모델링 #1
		* 진행: 스터디 구성 팀원 (3명 - Feature Engineering 1명, 분석모델 2명[선형 1, 트리 1])
		* 숙제: (스터디원 수준에 따라) BaseLine code Itermediate or 3rd_winner code
	* 3주차: 분석모델 모델링 #2
		* 진행: 스터디 구성 팀원 (3명 - Bagging과 Boosting & AdaBoost 1명, XgBoost 1명, LightGBM 1명)
		* 숙제: 2nd_winner
	* 4주차: 심화
		* 진행: 스터디 팀장님  (2명 - 상관관계 & 이상치 처리 심화 - 1명, 차원 축소 & high cat variable 처리 1명)
		* 숙제: 1st_winner

## :bus: 참여 대회명
제주 퇴근시간 버스승차인원 예측
	https://dacon.io/competitions/official/229255/overview/
	
## :books: 커리큘럼

### 1. 대회에 대한 이해 :grey_question:
 - 대회가 원하는 결과 알고리즘은?
	: 개요, 규칙, 데이터에 대한 개괄적인 이해
	(https://dacon.io/competitions/official/229255/overview/)
	
 - 분류 vs 회귀?
	: 지도학습의 대표적인 두가지 목표에 대한 이해

 - 회귀 측정지표에 대한 이해
	: 회귀 측정지표 종류, 지표별 사용 이유, 직접 만드는 나만의 측정지표
	
### 2. 탐색적 데이터 분석(EDA)
 - 탐색적 데이터 분석?
 
 - EDA에서 고려하는 것들
	1. 자료의 형태 이해
		: 범주형 - (명목형,순서형), 수치형 - (이산형,연속형)
		
	2. null값과 이상치

	3. 데이터 시각화
		* matplotlib.pyplot
		* seaborn
		* **3. plotly**

 - EDA를 활용한 퇴근시간 승차인원 데이터 셋 분석
 
### 3. Feature	 Engineering
 - 스케일링, 정규화
 - One-Hot Encoding
 - New feature creation
 
### 4. 분석모델 모델링
 - 머신러닝 기법
	1. 선형 모델
		: 릿지, 라쏘, 로지스틱 회귀
	2. 트리 모델
		: 결정 트리, 랜덤 포레스트
	3. Boosting 모델의 이해
	    * Bagging vs Boosting
		* AdaBoost
		* XgBoost
		* LightGBM
		
 - 교차검증(Cross vaildation)
 
### 5. 심화
 - Feature Engineering 심화
	1. 상관관계
	2. 이상치 처리 심화
		* Multiple Imputation
		* Regression Imputation
	3. 차원 축소
	4. high categorical variable 처리 방법
		* Mean Encoding
		* Frequency Encoding
		
 - 순위권 코드 심화
	: 스터디 진행 상황에 따라서 1,2,3등 코드 중 선정 및 클론코딩 진행
	
### 6. 고도화
	- Interpretable Machine Learning(lime)
		: 머신러닝/딥러닝 모델의 신뢰도에 대한 해석
		(http://research.sualab.com/introduction/2019/08/30/interpretable-machine-learning-overview-1.html)
	- Bayesian optimization
		: Model의 Hyperparameter를 튜닝하는데 사용
	- SHAP
		: 결과를 예측하는데 있어 Column의 영향도를 Insight