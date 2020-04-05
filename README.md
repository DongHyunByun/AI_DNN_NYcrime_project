# AI_DNN_NYcrime_project

1. **기간 : 2019.10~2019.11**

2. **기술스택 : python, pandas, numpy, tensorflow, keras**

3. **내용 :[뉴욕 범죄 데이터를 이용하여 **특정 시간**, **특정 범죄**가 **특정 자취구**의 "**어디서**" 발생할 것인지 예측]**
    1. 달,일,요일,시간,범죄장소,범죄종류가 나와있는 데이터를 이용
    2. 각각을 수치화
        - 시간 : 1월`~`12월->0~11, 1일`~`31일->0`~`30, 월`~`일->0`~`6, 0`~`23시->0`~`23
        - 범죄 : 교통법위반->0, 절도->1, 사기,위조,도박->2, 약물,술->3 ...
        - 도로번호 : 1`~`9->0, 10`~`19->1, 20`~`29->2 ...
    3. 5개의 자치구 중 도로번호가 1개로 분류되는 "STATEN ISLAND"를 제외한 4개의 도시로 분류
    4. 아래의 두가지 방법을 통해 DNN분석
        - 각 ATT를 그대로 one hot coding한 후 DNN분석  
        - 날짜와 범죄종류를 one hot coding한 뒤 DNN으로 분석
    5. 날짜 및 범죄 종류들을 **embedding하면 날짜사이의 상관관계에 따라 다른 가중치를 부여할 수 있다.**  
        - 수요일은 화요일과는 가깝고 일요일과는 멀다. 이러한 특징들을 반영할 수 있다.  
        - 참고  
        (https://medium.com/@davidheffernan_99410/an-introduction-to-using-categorical-embeddings-ee686ed7e7f9)  
        - 실제로 자치구 "queens"의 분석에서 embedding 후 DNN분석의 결과가 아래와 같이 개선된 형태로 나왔다.  
        **onehot-codding**  
        ![onehot](https://user-images.githubusercontent.com/50386280/78471226-a499c100-776a-11ea-94cc-5be7afcd8115.png)  
        
            **embedding**  
            ![embedding](https://user-images.githubusercontent.com/50386280/78471327-6d77df80-776b-11ea-8d77-681f18e1c4a6.png)

4. **파일설명**
    1. 1 범죄분류 확인  
        **[ input file : "NYPD_Complaint_Data_Current_YTD.csv", 설명 file : "범죄분류.xlsm" ]** 
        - input 데이터에 범죄 분류를 확인하고, 비슷한 범죄들을 어떻게 묶을지 판단.  
    2. 2 전처리  
        **[ input file : "each_city.folder", output file : "preprossed.folder"]**
        - 각각의 도시로 분류한 데이터들을 위에서 정한 수치화 기준에 맞기 수치화 한다.
    3. 3 DNN 분류  
        **[ input file : "preprossed.folder"]**
        - 전처리(수치화)된 지역별 데이터를 DNN분석한다.
        - model_embedding.ipynb는 데이터를 임베딩 후 DNN적용.
        - model_onehot.ipynb는 데이터를 전처리된 형태 그대로 DNN적용.
        
    
        
