# 데이터 모델링

<details><summary><h3>데이터 불균형 처리</h3></summary>

  -사건이 발생하지 않은 경우가 월등히 많아 undersampling 처리 후 변수명 변경
  ```
  from imblearn.under_sampling import NearMiss 
nm = NearMiss()

rus = RandomUnderSampler(random_state=0, sampling_strategy=0.7)
                         
        #                  {
        # 0: int(globals()["data_{}".format(i)][globals()["data_{}".format(i)]["label"] == 1].shape[0]*1.5),
        # 1: globals()["data_{}".format(i)][globals()["data_{}".format(i)]["label"] == 1].shape[0]})

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

<details><summary><h3>모델 선정 by Pycaret(AutoML)과 파라미터 튜닝</h3></summary>
-기계사고에 대한 Pycaret 결과 예시

![image](https://user-images.githubusercontent.com/111345469/224694243-b8acd554-0898-423b-80e9-948ba9f719ad.png)

각각의 사건에 대해 AutoML을 통해 점수를 확인하고 적합한 모델을 선정

```
# 각각의 모델 이름
RF_model = RandomForestClassifier(random_state = 10) # Random Forest
xgb_model = XGBClassifier(random_state = 10) # XGBoost
cat_model = CatBoostClassifier(random_state = 10) # CatBoost
```
  
</details>

<details><summary><h3>모델 학습 평가</h3></summary>
-# 기계사고 모델 roc_curve
![image](https://user-images.githubusercontent.com/111345469/224696625-7591d0bc-0fda-4b2e-9d15-c0771ff88ae6.png)

 -# 기계사고 모델 confusion


-# 기계사고 모델 feature importance

 -# 기타사고 모델 점수
</details>
