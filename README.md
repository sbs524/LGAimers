# LGAimers
LGAimers 3기 온라인 채널 제품 판매량 예측 AI 온라인 해커톤


## 🎶 Data Preprocessing
- 모든 데이터는 min-max scaling 으로 normalization 수행
- 추론 결과를 inverse scaling 하기 위해 max와 min값을 따로 저장
- train.csv(일별 판매량)에서 각 데이터 고유 번호인 ID, 제품 컬럼은 제외
- sales.csv(일별 총 판매금액)에서 train.csv와 중복되는 컬럼을 제외
- brand_keyword_cnt.csv(일별 브랜드 언급량)을 참조하여 나중에 train.csv파일에 이어 붙이기 위해 numpy 형태로 생성
- Label Encoding을 통해 문자열을 숫자로 변환

## 🎵Make train, predict data
- 각 데이터를 row에 날짜가 오도록 transpose하여 합침
- 사용자 지정된 학습날짜와 예측 날짜의 길이만큼 데이터를 분해
  
![image](https://github.com/sbs524/LGAimers/assets/80670002/04e74da2-e99b-4b9e-a111-2d3722f2e9cf)

## 🎸학습 알고리즘
CNN을 겹겹이 쌓아 데이터의 특징을 잡아낼 수 있도록 하였고
이를 거친 데이터를 LSTM을 통해 학습 시키도록 진행하였다.

- CNN과 LSTM을 결합한 LSTNet을 사용
- CNN 7층을 쌓고 도출된 결과를 다시 3개의 CNN을 통해 Convolution 진행
- 아래 그림과 비슷한 과정을 2번 거쳐서 결과를 도출

![image](https://github.com/sbs524/LGAimers/assets/80670002/f5f457a0-4d69-4e57-8343-c6abcaef92b4)
<br>출처 : https://paperswithcode.com/paper/modeling-long-and-short-term-temporal


## 🎧추론
- normalization시 저장해둔 max, min값을 통해 inverse scaling 진행
- 생성된 값을 반올림하여 정수형태로 반환
