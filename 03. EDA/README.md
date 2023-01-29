# EDA

<details><summary><h3>relationship_between_variables</h3></summary>

- **`일별 사건 발생 빈도 시각화`**
  - 365일 동안 일일 사건 발생 빈도 확인
  - ![일별 사건 발생 빈도](https://user-images.githubusercontent.com/95950967/215325904-4a24b435-1a50-4842-9a97-805d64797743.png)
  
- **`유동인구와 사건의 연관성 시각화`**
  - 사건이 발생 한 장소에 대한 유동인구 비율 시각화 
  - ![유동인구와 사건의 연관성](https://user-images.githubusercontent.com/95950967/215325955-2f5c16a8-a930-456d-99db-fe1738355cb1.png)
  
- **`날짜와 사건의 연관성 시각화`** 
  - 월, 일, 요일, 계절의 각 요소별로 사건과의 연관성을 확인
  - 아래의 사진의 경우 4가지중 월에 해당하며, 추가적인 EDA는 코드를 참고
  - 1의 경우 사건이 발생, 0의 경우 사건이 발생하지 않은 경우를 시각화
  - ![월별 사건 발생 현황](https://user-images.githubusercontent.com/95950967/215326097-fe1b77a0-60f1-4d06-897f-d906b1aab58c.png)
  
- **`휴가철 사건 발생 현황 시각화`** 
  - 휴가철의 경우 평소보다 유동인구 변동이 크며, 사건이 많이 발생할 것으로 예상되기에 시각화
  - ![휴가철 사건 발생](https://user-images.githubusercontent.com/95950967/215326349-57bc7b79-828f-4d19-8c31-203ed3ff3c3e.png)
  
- **`기상조건과 사건발생의 연관성 시각화`** 
  - 온도, 강수량, 적설량, 풍속, 습도의 각 요소별로 사건과의 연관성을 확인
  - 아래의 사진의 경우 4가지중 적설량에 해당하며, 추가적인 EDA는 코드를 참고
  - 1의 경우 사건이 발생, 0의 경우 사건이 발생하지 않은 경우를 시각화
  - ![다운로드](https://user-images.githubusercontent.com/95950967/215326449-4ca132a9-8a70-4596-8070-ef96246ed691.png)
  
</details>

<details><summary><h3>Geospatial_Data_Visualization</h3></summary>

- **`격자별 사건의 빈도수화`**
  - 주어진 GPS 좌표 KATEC을 변환 함수를 사용하여 WGS804로 변경
  - 각 건수별로 색을 나눠서 원주 격자 좌표화를 통한 공간정보 시각화
    - 70건 이상 : 빨간색
    - 30건 이상 : 주황색
    - 10건 이상 : 노랑색
    - 1건 이상 연두색
    - 0건 : 회색
    - 유동인구 0이며 사건이 0건인 경우 색 X
  - 주로 사건이 발생되는 장소 : 원주 기업도시 / 원주 도심지역 / 문막읍 / 흥업리 / 신림면 / 태장농공단지를 확인
  - ![사건의 빈도수화](https://user-images.githubusercontent.com/95950967/215327009-c44e1dee-b7fd-4439-92b7-ae80788ff59b.png)
  
</details>

<details><summary><h3>Influencing_Variables</h3></summary>
  
  - 각 데이터에 있는 주소값을 카카오 Api를 사용하여 위도, 경도 추출
  
  - 각 격자에 해당하는 위도, 경도를 함수를 이용하여 배분한다음 각 격자별로 사건 발생 유무 확인 
  
  - **`산업단지`**
    - ![다운로드 (5)](https://user-images.githubusercontent.com/95950967/215327795-19543188-37e8-43ca-80db-61241730990f.png)

  - **`유흥가 및 단란주점`**
    - ![다운로드 (6)](https://user-images.githubusercontent.com/95950967/215327797-71cafec0-911a-4da9-bf2e-83e59012c751.png)

  - **`경로당`**
    - ![다운로드 (7)](https://user-images.githubusercontent.com/95950967/215327798-60f33aa1-bda2-4722-950c-1d24addd0396.png)

  - **`음식점`**
    - ![다운로드 (8)](https://user-images.githubusercontent.com/95950967/215327799-ce9d255f-6ab2-414d-b83b-672e87cbbe44.png)
  
  - **`건축허가`**
    - ![다운로드 (9)](https://user-images.githubusercontent.com/95950967/215327801-87006c8f-7214-4e35-9a20-7070f0155036.png)

  - **`교통사고`**
    - ![다운로드 (10)](https://user-images.githubusercontent.com/95950967/215327802-ad19dc95-189c-4d4b-8acc-37980ab675f8.png)  

</details>
