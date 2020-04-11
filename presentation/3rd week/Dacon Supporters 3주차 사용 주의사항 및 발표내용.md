# Dacon Supporters 3주차 사용 주의사항 및 발표내용



## 사용 주의사항

본 .ipynb 파일은 **Google Colaboratory** 환경에서 작성되어 있으므로, 세번째 커널에 정의되어 있는 **'IS_COLAB'변수를 False로 변경**하고, **False에 해당하는 path변수**를 로컬 PC에 저장해둔 data 폴더의 디렉터리를 True일 때와 유사한 형태로 **정의합니다.**



## 구성 데이터 셋

1. train.csv / test.csv

   : 기본 훈련, 테스트 데이터

2. bus_bts.csv

   : 버스 승차 데이터

3. jeju_financial_life_data.csv

   : 제주도 금융 데이터

4. 행정\_법정동_중심좌표.csv

   : 행정 / 법정동 중심좌표 데이터

5. weather.csv

   : Winner Code의 날씨 Crawling Error 수정하여 추출한 날씨 데이터

6. OLS_coef_corr_90.csv

   : 상관계수가 절대값 0.9 이상인 경우를 제거한 독립변수들의 상관계수, OLS 회귀추정 가중치 값

7. Colinearity_90_VIF.csv
   : 상관계수가 절대값 0.9 이상인 경우를 제거한 독립변수들의 VIF 값

8. VIF_10_coef_corr.csv

   : 상관계수가 절대값 0.9 이상인 경우를 제거한 독립변수에서, VIF 값이 10이하인 컬럼들만 소거법으로 남긴 독립변수들의 상관계수, OLS 회귀추정 가중치 값

9. VIF_10_Selected_VIF.csv

   : '8'의 경우에서 도출한 VIF Factor 값을 저장

10. PermutaionImportance_REF.csv

   : Permutation Importance 방식을 활용하여 Selection한 컬럼들을 남겨둔 데이터셋

11. SHAP_REF.csv

   : SHAP 방식을 활용하여 Selection한 컬럼들을 남겨둔 데이터셋

## 발표 내용 서술

### <a href="https://www.kaggle.com/willkoehrsen/introduction-to-feature-selection">Feature Selection</a>

    참고자료
    https://www.kaggle.com/willkoehrsen/introduction-to-feature-selection
    : Feature Selection을 수행하는 절차
    http://wolfpack.hnu.ac.kr/lecture/Regression/ch6_multicollinearity.pdf
    : 다중공선성 문제를 해결하는 방법
    https://www.kaggle.com/harangdev/feature-selection
    : Feature Selection 실습


EDA를 통해 다양한 의미 있고 다양한 Feature를 생성하는 것도 중요하지만, 실제 모델에 투입할 때 최적의 컬럼셋은 무엇일지를 결정하는 Selection 과정도 중요하다. generation한 만큼 연산에 무리가 있기 때문에 최적의 컬럼 수로 최고의 결과를 낼 수 있도록 해야 할 것이다. 

참조한 Feature Selection 관련한 방법은 크게 두 가지이다.

1. 독립 변수간 Colinearlity를 활용한 Selection

  * <a href="http://wolfpack.hnu.ac.kr/lecture/Regression/ch6_multicollinearity.pdf">다중공선성 문제를 해결하는 방법</a>

    1. 독립 변수간 높은 상관관계의 변수제거
    2. 주성분분석이용
    3. 능형회귀분석 이용



2. <a href="https://www.kaggle.com/harangdev/feature-selection">RFE를 활용한 Treemodel의 결과로 산출되는 Feature importance를 활용한 Selection</a>

  * 기본 Tree model의 Feature Importance
  * Permutational Importance
  * SHAP
  * boruta




####  1. 독립 변수간 Colinearlity를 활용한 Selection

<a href="https://m.blog.naver.com/PostView.nhn?blogId=vnf3751&logNo=220833952857&proxyReferer=https%3A%2F%2Fwww.google.com%2F
">**다중공선성(Multicollinearity)**</a>

    참고자료
    1. https://m.blog.naver.com/PostView.nhn?blogId=vnf3751&logNo=220833952857&proxyReferer=https%3A%2F%2Fwww.google.com%2F
    : 다중공선성의 정의와 OLS 회귀 추정에서 T-value와 p-value의 관계에 대해 쉽게 설명해둠
    2. https://bkshin.tistory.com/entry/DATA-20-%EB%8B%A4%EC%A4%91%EA%B3%B5%EC%84%A0%EC%84%B1%EA%B3%BC-VIF
    : 다중공선성을 검증을 위한 VIF 값 활용
    3. https://datascienceschool.net/view-notebook/36176e580d124612a376cf29872cd2f0/
    : 다중공선성검증을 위한 VIF 값 활용 실습


일반적으로 회귀 분석에서는 어떤 설명 변수의 영향력을 파악할 때
다른 설명 변수들을 모두 일정하다고 생각하고 검증합니다. 즉, 설명 변수들끼리 서로 독립이라는 가정을 하는 것이죠. 그래야 알아보고자 하는 변수의 영향력만을 오롯이 알 수 있기 때문입니다. 하지만 만약 어느 두 설명 변수가 서로에게 영향을 주고 있다면?
올바른 회귀선을 그릴 수 없게 됨. 왜냐하면 회귀 분석의 전제를 위반하는 행위이기 때문이다. 그러므로 우리는 두 독립변수 간에 발생하는 다중 공선성을 제거해야 한다.

**다중공선성을 제거하는 방법**

1. 일차적으로 독립 변수간에 상관계수가 높은 값을 기준으로 컬럼을 drop
2. 상관계수와 함께 VIF(Variable Inflation Factor)를 활용한 컬럼 drop

  다중 공선성을 없애는 가장 기본적인 방법은 다른 독립변수에 의존하는 변수를 없애는 것이다. 가장 의존적인 독립변수를 선택하는 방법으로는 VIF(Variance Inflation Factor)를 사용할 수 있다. VIF는 독립변수를 다른 독립변수로 선형회귀한 성능을 나타낸 것이다.  i 번째 변수의 VIF는 다음과 같이 계산한다.

  <img src="https://lh3.googleusercontent.com/proxy/hFGWIpyRJ3vcwTNSVkDSsOs_toivJL0e6bGOXFgf2h6OfEA3xJLm0zZYv3XNbaITz51az_gO_uQdjaLu9WGCJHirPLeZtMQhdn-s2NTxs6MlhF5AGW-aXSW66gBV0VuLLOy1S0-cv-LENfxx5dw8j0xoeLIZtbQ4B08" width=150 />



###### **|Corr| < 0.9 OLS 회귀 추정 결과 분석**

회귀분석은 앞서 말했듯이, 독립변수간의 상관관계가 완전 독립인 경우를 가정하고 계산을 진행하여 가중치를 계산하게 된다. 만약 회귀계산식이 잘못된 경우에는 도출한 가중치 w값과 두 변수간의 상관계수의 값이 서로 다른 부호를 나타낸다. 

아래의 결과도, 일차적으로 높은 상관관계(90%이상)를 가진 컬럼을 제거했음에도 일치하지 않는 것을 볼 수 있고, 이를 VIF Factor를 통해 검증했을 때도, 10이상의 값을 가진 컬럼은 43개 정도 됨을 알 수 있다.




#####  VIF 지표를 활용한 컬럼 삭제

VIF 지표를 활용한 컬럼을 삭제할 때는, 계산시 특정 임계점 이상의 값을 한꺼번에 삭제하는 것이 아니라, 가장 높은 값의 VIF 변수부터 차례대로 삭제해 나가야한다. 

그러므로 아래의 코드는 아래와 같은 메커니즘으로 움직인다.

1. 타겟값을 제외한 나머지 독립변수를 활용하여 OLS 회귀 추정 및 상관계수 값을 계산한다.
2. 두 값을 비교하여, 부호 간의 차이가 발생하면, VIF Factor 계산을 실시하고, 없다면 멈춘다.
3. VIF Factor를 계산하고 임계점 이상을 넘기는 값들 중 가장 높은 값을 가지는 컬럼을 제거하며, 동일한 값을 나타내는 경우, 타겟 컬럼과의 상관계수가 낮은 컬럼을 제거한다.
4. 1~3을 반복하게 되며, VIF Factor 값의 임계치를 넘는 값이 없는 경우 멈춘다.



​	**컬럼 Selection 결과**

```
number of columns: 66
remained columns: ['6~7_ride', '9~10_ride', '11~12_ride', '6~7_takeoff', '9~10_takeoff', '11~12_takeoff', 'day', 'Mon', 'Sat', 'Thr', 'Tue', 'is_holiday', 'in_out_8~9_takeoff_mean', 'dis_jeju', 'dis_seongsan', 'dis_po', 'gosan', 'po', '7~8_ride_date_sum', '6~8r', '8~10r', '10~12r', '8~10t', '10~12t', 'bus_route_id_mean', 'station_code_mean', 'station_code_sum', 'route_station_code_mean', 'congestion', '6~7_ride_sum', '7~8_ride_sum', '8~9_ride_sum', '9~10_ride_sum', '10~11_ride_sum', '11~12_ride_sum', '6~7_takeoff_sum', '7~8_takeoff_sum', '8~9_takeoff_sum', '9~10_takeoff_sum', '10~11_takeoff_sum', '11~12_takeoff_sum', 'user_cat_sum_2', 'user_cat_sum_4', 'user_cat_sum_30', 'user_cat_ratio_2', 'user_cat_ratio_4', 'user_cat_ratio_6', 'user_cat_ratio_27', 'user_cat_ratio_28', 'user_cat_ratio_29', 'user_cat_ratio_30', '현재기온_10', '일강수_10', 'is_rain', '구름많음', '구름조금', '맑음', '박무', '보통비계속', '비 끝남', '소나기 끝', '약한비계속', '약한비단속', 'encoded_bus_route_id_frequency_encoded', 'encoded_station_code_frequency_encoded', 'encoded_route_station_code_frequency_encoded']
```



###### VIF Factor를 활용한 다중공선성 제거 결과 확인

1. 부호간의 차이를 보이큰 컬럼은 제거 전과달리 39개에서 24개로 줄어들었다.
2. VIF Factor가 10을 넘는 컬럼은 이제 없다.

1번의 경우가 발생한 것으로 보아, 아직 약간의 공선성이 발생하고 있는 것으로 보이나, 처음 무한대의 VIF 값을 가진 것과 달리 10을 넘기는 컬럼값은 삭제가 되었다.




#### 2. RFE를 활용한 Treemodel의 결과로 산출되는 Feature importance를 활용한 Selection

#####  Permutation Importance


	https://www.kaggle.com/dansbecker/permutation-importance
	: Permutation Importance 정의 및 실습(영문)
	https://www.kaggle.com/harangdev/feature-selection
	: Permutation Importance 실습
	https://eli5.readthedocs.io/en/latest/blackbox/permutation_importance.html
	: Permutation Importance 공식문서(영문)
	https://tootouch.github.io/IML/permutation_feature_importance/
	: Permutation Importance 란? (한글 번역본)



Permutation Importance는 '특정 feature를 사용불가능 상태로 만들었을 때 얼마나 예측점수가 감소했는지'를 활용하여 Importance를 측정합니다. 예를들어 X1~10까지의 독립변수가 있으며, 하나의 컬럼을 제거해가면서 학습을 하여 중요도를 측정하는 방식입니다. 하나의 컬럼을 제거 했을 때, 점수의 감소폭이 크다면, 그 컬럼은 결과값을 유추하는데 중요도가 큰 컬럼이 되는 것입니다. 

<img src="https://i.imgur.com/h17tMUU.png" width=800 />

그런데 하나의 컬럼을 없애고 학습한다는 것은, 매번 컬럼을 제거하고 학습을 진행하기 때문에 매번 새로운 학습을 시켜야하는 문제점이 있습니다. 이때는 ***\*제거해야할 컬럼을 random 하게 셔플함(Random Noise)으로써\**** 학습에 대한 내용을 '무력화'시키는 것입니다. 

그러나 해당 방법으로 컬럼을 계산하는것은 많은 Computing Power를 요함.

