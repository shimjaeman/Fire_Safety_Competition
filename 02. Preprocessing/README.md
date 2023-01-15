# Preprocessing

<details><summary><h3>Less_related_to_accident</h3></summary>

- **`격자 위치별 사고 발생 확인`**
  - 1건이상 발생한 사고 격자별로 사건 건수를 합친것을 이용하여 각 사고별 격자위치 확인
  - 사고가 자주발생하지 않는 격자나 특정 사고가 발생하는 격자가 있을것이라 생각
  - ![격자 위치별 사고 발생](https://user-images.githubusercontent.com/95950967/212538907-14419ee4-3a50-4afe-b749-877bd7764b79.png)

- **`사고 제거 리스트`** : 발생요일에 관한 정보  
  - 15개 이하로 발생한 사고의 경우 위 격자를 확인 한 결과 우연에 의한 사고일 가능성이 높기에 제거
  - 사고 제거 리스트
    - HGTPOJ_ACDNT_OCRN_CNT : 고온체사고발생건 ----> 4건
    - PNTRINJ_OCRN_CNT : 관통상발생건수 ----> 1건
    - AGRCMCHN_ACDNT_OCRN_CNT : 농기계사고발생건수 ----> 0건
    - UNKNWN_OCRN_CNT : 미상발생건수 ----> 5건
    - THML_DAMG_OCRN_CNT : 온열손상발생건수 ----> 6건
    - DRWNG_OCRN_CNT : 익수발생건수 ----> 13건
    - PRGNTW_ACDNT_OCRN_CNT : 임산부사고발생건수 ----> 8건
    - ELTRC_ACDNT_OCRN_CNT : 전기사고발생건수 ----> 1건
    - ASPHYXIA_OCRN_CNT : 질식발생건수 ----> 11건
    - FLAME_OCRN_CNT : 화염발생건수 ----> 4건
    - CHMC_SBSTNC_ACDNT_OCRN_CNT : 화학물질사고발생건수 ----> 1건
    - WETHR_ACDNT_OCRN_CNT : 날씨사고발생건수 ----> 0건
    - SXAL_ASALT_OCRN_CNT : 성폭행발생건수 ----> 0건
    - BURN_OCRN_CNT : 화상발생건수 ----> 2건
  
- **`ZERO 격자 제거`** 
  - 사고가 발생하지 않으면서 유동인구가 0인 행 제거
</details>

<details><summary><h3>Date</h3></summary>

- **`MONTH`** : 발생월에 관한 정보
  
- **`DAY`** : 발생일에 관한 정보

- **`WEEKDAY`** : 발생요일에 관한 정보  
  - 각 요일별(평일, 주말) 사고 발생이 다를것이라고 생각
  
- **`SEASON`** : 발생계절에 관한 정보
  - 계절과 사고의 연관성을 확인하기 위하여 추가
  - SPRING : 1  [3,4,5]
  - SUMMER : 2  [6,7,8]
  - AUTUMN : 3  [9,10,11]
  - WINTER : 4  [12,1,2]

- **`HOLIDAY`** : 휴일여부에 관한 정보
   - 휴가철 사고발생 건수가 평상시 대비 증가하기 때문에 휴일여부 추가
   - ![추석연휴기간 일평균 사고 발생현황](https://user-images.githubusercontent.com/95950967/212538465-fb176422-4015-46f1-b27f-bf67823ce2bc.png)
  - 0 : 평일 / 1 : 공휴일 (2021년도 대체공휴일 포함)
    
</details>

<details><summary><h3>Weather</h3></summary>
  
- **`가설`** : 해당 변수들은 낙상 및 교통사고 등의 사고에 많은 영향을 주는 변수일 것이다. 

- **`AVRG_TMPRT`** : 평균기온(°C)에 관한 정보
  
- **`DAY_RAINQTY`** : 강수량(mm)에 관한 정보

- **`DAY_MSNF`** : 적설량(cm)에 관한 정보 
  
- **`AVRG_WS`** : 평균 풍속(m/s)에 관한 정보

- **`AVRG_HUMIDITY`** : 평균 습도(%)에 관한 정보
    
</details>

<details><summary><h3>Derived_Variables</h3></summary>
  
- **`가설`**  : 65세 이상 고령자의 안전사고가 매년 증가하고 있으므로 발생 횟수에 영향을 미칠 것이다.

- ![65세 이상 고령자 사고현황](https://user-images.githubusercontent.com/95950967/212539956-2cf13929-dea0-497c-a936-32711dd80ed3.png)

    
</details>

<details><summary><h3>Asymmetric_Data_Normalization</h3></summary>
  
- **`비대칭 데이터 확인`** 
  - 비대칭 값(skew)가 절대값 0.5 안에 들어오지 않은 데이터를 확인
  - ![Box-Cox Transform 처리 전 분포 확인](https://user-images.githubusercontent.com/95950967/212539482-38204e56-050c-4e88-ad40-969f3215b11b.png)
  
- **`비대칭 정규화 수행`**
  - ![Box-Cox를 Transform 한 후 분포 확인](https://user-images.githubusercontent.com/95950967/212539505-3a8b46c0-1787-4133-abbf-d42589abdb40.png)
    
</details>

<details><summary><h3>Final_Preprocessing</h3></summary>
  
- **`데이터 스케일링`** 
  - ![스케일링 후 변수 분포 확인](https://user-images.githubusercontent.com/95950967/212539746-a8c1935c-7ed1-4b21-b61a-4d3774b249cc.png)

  
- **`모델에 사용하는 최종 독립 변수`**
  - MONTH : 월
  - DAY : 일
  - WEEKDAY : 요일
  - HOLIDAY : 공휴일
  - SEASON_SE_NM : 계절
  - AVRG_TMPRT : 평균기온(°C)	
  - DAY_RAINQTY : 일강수량(mm)
  - DAY_MSNF : 일적설량(cm)
  - AVRG_WS : 평균 풍속(m/s)
  - AVRG_HUMIDITY : 평균 습도(%)
  - INDUSTRIAL_CNT : 격자내 산업단지 개수
  - BAR_CNT : 격자내 유흥업소 개수
  - SENIOR_CENTER_CNT : 격자내 경로당 개수
  - RESTAURANT_CNT : 격자내 식당 개수
  - BULID_PERMIT_CNT : 격자내 건축허가 개수
  - ACCIDENT_AREA_CNT : 격자내 사고건수
  - ALL_POP : 전체 연령(65세 미만) 유동인구
  - ELDER_POP : 65세 이상 유동인구
  - GRID_ID : 격자 ID    
  
- **`모델에 사용하는 최종 종속 변수`**
  - MCHN_ACDNT_OCRN_CNT : 기계사고발생건수
  - ETC_OCRN_CNT : 기타발생건수
  - BLTRM_OCRN_CNT : 둔상발생건수
  - ACDNT_INJ_OCRN_CNT : 사고부상발생건수
  - EXCL_DISEASE_OCRN_CNT : 질병외발생건수
  - VHC_ACDNT_OCRN_CNT : 탈것사고발생건수
  - HRFAF_OCRN_CNT : 낙상발생건수
  - DRKNSTAT_OCRN_CNT : 단순주취발생건수
  - ANML_INSCT_ACDNT_OCRN_CNT : 동물곤충사고발생건수
  - FLPS_ACDNT_OCRN_CNT : 동승자사고발생건수
  - PDST_ACDNT_OCRN_CNT : 보행자사고발생건수
  - LACRTWND_OCRN_CNT : 열상발생건수
  - MTRCYC_ACDNT_OCRN_CNT : 오토바이사고발생건수
  - DRV_ACDNT_OCRN_CNT : 운전자사고발생건수
  - BCYC_ACDNT_OCRN_CNT : 자전거사고발생건수
  - POSNG_OCRN_CNT : 중독발생건수
  - FALLING_OCRN_CNT : 추락발생건수

- **`Undersampling 처리`**
  - 데이터 그대로 진행할시 0값에 데이터가 몰려있어 undersampling 처리 후 변수명 변경

</details>


