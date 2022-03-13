# DACON 뉴스 토픽 분류 AI 경진대회 (NLP 분반)
- 뉴스 제목 데이터를 통해 뉴스의 주제를 분류하는 Classification 모델 구현
- Back Translation을 이용해 증강한 데이터를 훈련에 사용, 다수의 RoBERTa 모델을 앙상블함.
- PPT [Link](https://github.com/KU-BIG/KUBIG_2022_SPRING/blob/main/KUBIG%20Contest/NLP/nlp_KUBIG%20CONTEST.pdf)

# EDA
- Target 분포 확인                                              
                           
![image](https://user-images.githubusercontent.com/95842327/158068460-1e9f409d-84c7-472a-a609-5e0911b495ad.png) 


- 한자어 존재하는 데이터 다수 확인

![image](https://user-images.githubusercontent.com/95842327/158068644-c02e257b-2345-4445-9a6c-c08d1615e6c8.png)

# PreProcessing
- 한자어 번역 : 빈도 10 이상의 한자어에 대해 번역 실행.
![image](https://user-images.githubusercontent.com/95842327/158069332-d3119132-b1ba-4326-ab5e-eff4bc6de103.png)
![image](https://user-images.githubusercontent.com/95842327/158068754-5d269556-385b-4ade-8727-8bdac442d5fd.png)

- 역번역 (Back Translation) : 과적합 방지 등을 위한 Data Augmentation으로,
  데이터를 한 -> 영 -> 한 으로 번역하여 노이즈가 추가된 텍스트를 학습에 추가로 사용.
- 네이버의 PAPAGO를 크롤링하여 사용.
- Code [Link](https://github.com/KU-BIG/KUBIG_2022_SPRING/blob/main/KUBIG%20Contest/NLP/train%20set%20%E1%84%92%E1%85%A1%E1%86%B8%E1%84%8E%E1%85%B5%E1%84%80%E1%85%B5%2C%20test%20%E1%84%87%E1%85%A5%E1%86%AB%E1%84%8B%E1%85%A7%E1%86%A8.ipynb)
# Modeling
- RoBERTa 모델 : 기존 Bert 모델의 보완으로, 한국어 자연어 데이터셋 
   KLUE (Korean Language Understanding Evaluation) 로 사전 학습된 모델을 파인 튜닝하여 사용.
-  DistilRoBERTa, klue/roberta-small/base, roberta-small, bert-base 등 다양한 모델을 사용하였고, 
   총 4개의 모델을 Soft Voting의 방법으로 Ensemble하여 최종 결과 도출. 
# Result
- Public : 0.87009 (17위)
- Private : 0.83552 (8위) 

# 기타 LINK
- 전처리 및 번역 Code [Link](https://github.com/KU-BIG/KUBIG_2022_SPRING/blob/main/KUBIG%20Contest/NLP/train%20set%20%E1%84%92%E1%85%A1%E1%86%B8%E1%84%8E%E1%85%B5%E1%84%80%E1%85%B5%2C%20test%20%E1%84%87%E1%85%A5%E1%86%AB%E1%84%8B%E1%85%A7%E1%86%A8.ipynb)
- 영어 번역 데이터만 이용한 RoBERTa 모델 Code [Link](https://github.com/KU-BIG/KUBIG_2022_SPRING/blob/main/KUBIG%20Contest/NLP/%E1%84%8B%E1%85%A7%E1%86%BC%E1%84%8B%E1%85%A5%E1%84%87%E1%85%A5%E1%86%AB%E1%84%8B%E1%85%A7%E1%86%A8%E1%84%87%E1%85%A9%E1%86%AB%20robert%20modeling.ipynb)
