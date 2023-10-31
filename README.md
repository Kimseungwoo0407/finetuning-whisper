# 졸업 논문 과제 수행

# 사용 데이터
AIhub에서 제공한 어린이 음성 데이터 셋

https://aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&dataSetSn=71502


# 필요성
- 대부분의 음성 인식 모델은 어른 음성 데이터에 초점이 맞춰져 있고, 어린이들의 경우 어린이 예능을 시청할 때 자막이 없으면 내용 이해가 어려움


# 기대효과
- 어린이 대상 제품 및 서비스 개선
- 다시 보기 자막 생성
- 어린이 콘텐츠 이해도 향상


# 발전 계획
- 더욱 정확한 음성 인식이 되기 위해 사용하지 않은 어린이 음성 데이터 추가




# 데이터셋 구축
### Aihub에서 제공하는 어린이 방송 음성/맥락 데이터 셋 활용

- 어린이 방송 음성/맥락 데이터 : 20,000건의 WAV와 JSON 형식으로 구성

- 카테고리 : 미취학 아동 발달 교육, 어린이 교육, 어린이 드라마, 어린이 예능

- 대화 주체 : 어린이 <-> 성인 (약 96%), 어린이 <-> 어린이 (약 4%)로 구성

- 카테고리 중 어린이 예능 음성/맥락 데이터 셋 활용

- 자연스러운 언어 사용 패턴과 감정을 잘 반영할 수 있을 것 같아 선정

- 130건의 WAV와 JSON 파일을 활용


### 데이터 전처리
- 데이터셋 준비.ipynb 에서 확인


## Whisper 모델을 fine-tuning 하여 어린이 음성 인식에 특화된 whisper 개발


### 모델 선정 이유
- Whisper는 특이한 액센트나 강한 배경 소음과 같은 어려운 환경에서 효과적으로 음성을 인식할 수 있는 능력을 갖추고 있음

- 어린이 예능의 경우 배경 음악이 깔리는 경우가 많아 , Whipser 모델이 적합하다고 생각
 
- 다국어를 지원하는 모델 ( 한글 지원 )



## Fine-tuning
- finetuning-whisper.ipynb 에서 확인


### WER vs CER ( 평가 지표 )
- WER

＇하였습니다＇라는 한 단어는 ＇하＇, ＇였＇, ＇습니다＇라는 세 개의 형태소로 구성되어 있다. 
만약 ＇하였습니다＇를 ＇했습니다＇로 인식한다면, 단어 단위로 보면 
완전히 다른 단어로 인식한 것이므로 오류율은 100%가 된다.

- CER

(S + D + I) / N = (S + D + I) / (S + D + C) = (1 + 1 + 0) / (1 + 1 + 3) = 0.4 즉, 40%가 된다.

'하였습니다'의 '하'를 '했'으로 대체하면 대체(S)가 1회 발생 
그리고 '였'이 삭제되어야 하므로 삭제(D)도 1회 발생 
추가로 삽입되는 문자(I)는 없음
따라서 정확한 문자 수(C)는 ＇습＇, ＇니＇, ＇다＇인 3개의 문자가 정확하게 대응됨



### 평가 결과

![image](https://github.com/kimseungwoo99/fine-tuning-whisper/assets/120182622/4f6e4f31-3e1c-4b46-a6a0-b27b922c618b)



### 모델 사용 ( colab이 아닌 jupyter notebook에서 사용 )

using-whisper.ipynb 확인
![image](https://github.com/kimseungwoo99/fine-tuning-whisper/assets/120182622/0ee29933-dda7-4b76-b7d0-9e5f7b25f34c)



#### 출처

https://www.louisbouchard.ai/whisper/

https://openai.com/research/whisper

https://aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&dataSetSn=71502

https://huggingface.co/blog/fine-tune-whisper#introduction

https://huggingface.co/spaces/evaluate-metric/cer

https://velog.io/@mino0121/NLP-OpenAI-Whisper-Fine-tuning-for-Korean-ASR-with-HuggingFace-Transformers


