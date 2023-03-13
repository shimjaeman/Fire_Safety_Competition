# 데이터 모델링

<details><summary><h3>데이터 변수명 지정 및 불균형 처리</h3></summary>
  
- **데이터 변수명 지정**
  
```python
# 분석할 17개의 사고의 변수명 지정 
col = ['MCHN_ACDNT_OCRN_CNT', 'ETC_OCRN_CNT', 'BLTRM_OCRN_CNT',
       'ACDNT_INJ_OCRN_CNT', 'EXCL_DISEASE_OCRN_CNT', 'VHC_ACDNT_OCRN_CNT',
       'HRFAF_OCRN_CNT', 'DRKNSTAT_OCRN_CNT', 'ANML_INSCT_ACDNT_OCRN_CNT',
       'FLPS_ACDNT_OCRN_CNT', 'PDST_ACDNT_OCRN_CNT', 'LACRTWND_OCRN_CNT',
       'MTRCYC_ACDNT_OCRN_CNT', 'DRV_ACDNT_OCRN_CNT', 'BCYC_ACDNT_OCRN_CNT',
       'POSNG_OCRN_CNT', 'FALLING_OCRN_CNT']

for i in col: # 변수명 지정 --> data_각 사고 이름 ( ex) data_HRFAF_OCRN_CNT )
    globals()["data_{}".format(i)] = pd.DataFrame()
    globals()["data_{}".format(i)] = final_DF.iloc[:,18:] # X 값
    globals()["data_{}".format(i)]["GRID_ID"] = final_DF["GRID_ID"]
    globals()["data_{}".format(i)]["label"] = final_DF[i] # 라벨 넣기
  
  
  ```
  
  
  
 
  
  
  - **사건이 발생하지 않은 경우가 월등히 많아 undersampling 처리 후 변수명 변경**
  ```python
from imblearn.under_sampling import NearMiss 
nm = NearMiss()

rus = RandomUnderSampler(random_state=0, sampling_strategy=0.7)
                         


for i in col: 
    X = globals()["data_{}".format(i)].iloc[:,:-1] 
    y = globals()["data_{}".format(i)]["label"]
    
    globals()["res_X_{}".format(i)], globals()["res_y_{}".format(i)] = rus.fit_resample(X, y) ###

    globals()["res_X_{}".format(i)]["label"] = globals()["res_y_{}".format(i)]
    globals()["res_{}".format(i)] = globals()["res_X_{}".format(i)]

    
    X = globals()["res_{}".format(i)].drop(['label'], axis=1)
    y = globals()["res_{}".format(i)]['label']
    
    # 각 사건 변수 훈련 데이터 / 테스트 데이터 분리
    globals()["X_train_{}".format(i)], \
    globals()["X_test_{}".format(i)], \
    globals()["y_train_{}".format(i)], \
    globals()["y_test_{}".format(i)] = train_test_split(X, y, test_size = 0.3, random_state = 0)
  ```
  
</details>

<details><summary><h3>모델 선정과 파라미터 튜닝</h3></summary>
  

- **AutoML을 통해 점수를 확인하고 적합한 모델을 선정**
![image](https://user-images.githubusercontent.com/111345469/224694243-b8acd554-0898-423b-80e9-948ba9f719ad.png)
  
기계사고에 대한 Pycaret 결과 예시

- 사용할 모델트리스트
```python
RF_model = RandomForestClassifier(random_state = 10) # Random Forest
xgb_model = XGBClassifier(random_state = 10) # XGBoost
cat_model = CatBoostClassifier(random_state = 10) # CatBoost
  
```
이후 GridSearchCV 및 RandomSearchCV을 통해 파라미터 수정 진행
  
- 파라미터 예시
```python
  # CatBoost fit
def CatBoost_model(X_train, y_train, X_test):
    params = {
            "iterations" : 1000,
            "learning_rate" : 0.002,
            "depth" : 6,
            "l2_leaf_reg" : 3,
            "model_size_reg" : 0.5,
            "rsm" : 1,
            "loss_function" : "Logloss",
            "border_count" : 254,
            "feature_border_type" : "GreedyLogSum",
            "leaf_estimation_iterations" : 10,
            "leaf_estimation_method" : 'Newton',
            "class_weights" :None,
            "random_strength" :1,
            "eval_metric" : "Logloss",
            "boosting_type" :"Plain",
            "task_type" :"CPU",
            "subsample" : 0.8,
            "grow_policy" : "SymmetricTree",
            "min_data_in_leaf" :1,
            "max_leaves" :64,
             }
    CBCM = CatBoostClassifier(**params, random_state = 10)
    CBCM.fit(X_train, y_train)
    return CBCM
```
  
  
</details>

<details><summary><h3>모델 학습 평가</h3></summary>
  
- 기계사고 모델 roc_curve
  
![image](https://user-images.githubusercontent.com/111345469/224696625-7591d0bc-0fda-4b2e-9d15-c0771ff88ae6.png)

 - 기계사고 모델 confusion
![image](https://user-images.githubusercontent.com/111345469/224699475-2e1272d8-f6f1-4586-a353-34f385565a4d.png)

- 기계사고 모델 feature importance
![image](https://user-images.githubusercontent.com/111345469/224699585-b1177baf-a8a6-430c-bad4-63d5175b5806.png)

  노인 인구 밀집 지역에 많은 출동이 있었음을 알 수 있다.
  
  (위와 같은 작업을 각 사건에 대해서 진행)
  
</details>
