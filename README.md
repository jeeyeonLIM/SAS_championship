
# [제 16회 SAS 분석 챔피언십](https://www.sas-analytics.co.kr/) (2018.07 ~ 2018.08) 
  - [주제정의서 & 평가기준](https://github.com/jeeyeonLIM/Career/files/4148426/16.SAS._.pdf)
   
## 분석 주제 및 목적 
- 분석 주제 
   - 1. 교통사고에 영향을 미치는 원인과 징후에 대한 탐색 및 시각화
   - 2. 교통사고 위험구간 예측을 위한 파생변수 생성 및 모델링
   - 3. 분석결과를 이용한 사고예방과 교통안전을 위한 방안 및 정책 제시
- 분석 목표 
   - 교통사고 이력, 디지털 운행기록(DTG), 교통 시설물 데이터 등을 이용하여 사고 발생에 영향을 미치는 요인을 탐색하고 사고와의 연관 관계를 규명, 도로구간에 어떤 사고가 발생할지 예측함
   - 분석 결과를 이용하여 현실적으로 적용 가능한 정책, 활용방안 제시

### 우리 팀의 세부 목표를 정리하면,
- 데이터 분석 시 무엇보다도 객관적인 사실에 근거한 분석을 했다. 따라서 다양한 참고 자료를 활용해서 기준을 선정해 분석에 반영했다.
    - `EX1.` 교차로 주변이 혼잡하여 교통사고가 증가할 것이라고 생각했고 이 기준을 정할 때에 있어서 왕복 2차선 도로의 도로 폭을 구글링을 통해 확인하고 이에 근거하여 반경을 설정함
    - `EX2.` CCTV의 영향을 보기 위하여 반경을 설정할 때 있어 논문([이건학,"공공 cctv의 공간 분포 특성과 가시 커버리지에 기반한 최적 입지"](http://kgeography.or.kr/homepage/kgeography/www/old/publishing/journal/53/03/08.pdf))을 보고 CCTV 영향력 범위가 통상적으로 '200M' 기준이라는 사실을 참고하여 반경 설정함 

---------------------------------

## 분석 과정 
### 1.분석 사용 변수 및 생성 과정
![](https://ifh.cc/g/p3eRQ.jpg)
- 아래 테이블은 `근방 시설물 수` 파생변수 생성에 대한 분류 기준 및 근거임
 ![](https://ifh.cc/g/LvjeH.jpg)
   
- 아래 테이블은 택시 DTG(Digital Tacho Graph, 디지털 운행기록장치ㅡ차량의 GPS위치, 속도, 이동거리 등을 기록한 로그 데이터) 데이터를 이용하여 파생변수를 생성한 과정을 나타냄 
 ![](https://ifh.cc/g/QyUcS.jpg)

 - 이때 변수간 상관관계를 확인하여 모델링에 반영함
 
### 2. 모델링

####  Y(종속변수) 
'사고 심각도'로 설정하였으며, 이 사고 심각도 지수는 교통사고 관련 분석에서 활용되며 기존 논문ㅡ[원문](https://www.kci.go.kr/kciportal/ci/sereArticleSearch/ciSereArtiOrteView.kci?sereArticleSearchBean.artiId=ART001458138)을 바탕으로 '지수'를 이용함 
<p align="center">
  <img width="700" height="250" src="https://ifh.cc/g/yJhHk.png">
</p>

#### 다중공선성 확인 
- 변수간 다중공선성을 확인해본 결과 변수간 상관관계가 대체적으로 높았기 때문에 GLM 모형에 Lasso Penalty 적용 고려함 
<p align="center">
  <img width="700" height="250" src="https://ifh.cc/g/XRPpW.png">
</p>

- 사용한 모형은 Gamma GLM, Gradient Boosting, Random Forest 이며, 각각의 해석은 ppt 자료 참고
- 세 가지 모형의 MSE를 비교한 결과, Random Forest 채택 

### 3. 활용 방안
- 분석 결과를 바탕으로 최종 모형(RF) 로부터 중요변수는 발생월, 시간대, 운전자 연령대, 교차로 수, 차종, 요일군, 급가속지수였으며 해당 변수가 교통사고에 영향을 미치는 정도가 크다는 해석이 가능하고, 이에 맞는 활용 방안을 제시함 
- 방안 제시 시 크게 도로 및 환경 요인 vs 사람 요인 vs 차량 요인 으로 나누어 활용 방안을 제시함 

#### (1) 도로 및 환경 요인
<p align="center">
  <img width="700" height="250" src="https://ifh.cc/g/sZH2E.jpg">
</p>

#### (2) 사람 요인
<p align="center">
  <img width="700" height="250" src="https://ifh.cc/g/aNIQp.jpg">
</p>

#### (3) 차량 요인
<p align="center">
  <img width="700" height="250" src="https://ifh.cc/g/zXQtY.jpg">
</p>


#### 분석 도구 
- SAS Viya
- SAS VDMML; SAS Visual Data Mining and Machine Learning
- SAS Visual Analytics
- `Code` : ppt 자료 끝에 Appendix로 첨부함

