# NLP (Natural language process)

컴퓨터가 사람의 언어를 알아 듣도록 하는 연구 <br>
자연어 처리 <= 컴퓨터 과학 + 인공지능 + 언어학

## 자연어 처리 업무와 난이도

쉬움
* 스펠링 체크
* 키워드 검사
* 유사어 감지

중간
* 웹사이트나 서류의 형태 해석
* 구문 해석

어려움
* 기계번역
* 감정분석
* 질의 응답
    * closed-domain : 정해진 분야의 질문
    * opened-domain : 열린 질문

### 어려움
언어, 상황, 환경, 지각 지식의 학습 등 표현의 복잡함 -> Rule 기반으로 무리? <br>
DNN 이 분산표현의 장점으로 모호하지만 풍부한 정보를 얻을 수 있다!

## 분포 가설
비슷한 문맥을 가진 단어는 비슷한 의미를 갖는다
* Count-based method
    단어, 문맥 출현 횟수를 세는 방법<br>
    ex) SVD(LSA)

* Predictive method
    단어에서 문맥 또는 문맥에서 단어를 예측하는 방법<br>
    ex) NPLM, word2vec<br>

### <strong> 문맥이란? </strong><br>
크기 2K+1 단어열에 대해 기준 단어 주변의 단어가 문맥
* 단어문맥 행렬
* 특이치분해 (저차원, 조밀한 벡터로 압축) - 행렬 분해
    * 단어 벡터 집합 : 단어별 분산표현의 집합

* 어휘 수 줄이기 - 유사도로 (Cosine 유사도)
    * w1, w2 가 유사하면 1
    * w1, w2 가 관련없으면 0
-> 계산량이 너무 많아 nm^2<br>


## NN으로 만들어내는 <strong>언어 모델 </strong>
단어열의 문법과 의미가 올바른 정도를 나타내는 확률을 계산하는 모델
* n-gram 언어 모델
계산량의 한계로 조건을 붙여 확률의 근사화

* 분산표현을 통해 언어모델에서 못 잡아주는 것도 잡아줌
유사한 문맥은 한쪽 확률이 높아지면, 다른 한쪽도 높아진다.
* 유사성을 고려, 일반화 능력을 향상 -> 분산표현으로 할 수 있는 일이 즉 NN

## 개요
컴퓨터(기계)가 사람의 말(자연어)을 이해하도록 하는 노력들 <br>
> 완전히 이해하지 못해도 컴퓨터가 대충 판단(평가) 할 수 있도록  word와 character 들을 수치적 embdding 하는 것에서 시작
## 자연어를 수치화하기
### one-hot-coding
고려할 단어 전체 set = dict 으로 생각 => bag of words  
> I was young
I : [1 0 0 0 0]
was : [0 0 1 0 0]
young : [0 0 0 0 1] <br>
이런 식으로 문장을 수치로 대입변환 후 각종 분류기로 판단

단점 : 글에서 반복되는, 많이 쓰이는 단어가 더 중요할 거 같은데 여기선 무시된다.

### tf-idf
여러 글에서 나오는 빈도와 특정 글에서 빈도수를 기반으로 단어의 중요도를 따지는 방법
> 많은 곳에서 나오는 단어는 중요도가 낮고(일반적) 특정 글에서 많이 나오는 단어는 중요도가 높을 것이다.  

단점 : 문맥(Context)를 무시한다.

### n-gram
연속되는 단어를 묶어서(어절로) 의미를 처리

### pos tagging(품사 태깅)
품사태깅을 거치면 다른 스타일로 쓰인 문장간의 유사도를 어느정도 뽑아낼수 있다.  <br>
> 한국어는 어절보다 형태소 단위로 분석하는 것이 더 정확 <br>
한국어를 어절 단위로 분석하면 너무나 많은 가짓수가 나오게 된다(교착어). 따라서 형태소 단위로 분류하는게 좋다.

## 수치화된 문장을 분류하는 방법
* Naive Bayes  
* decision tree
* logistic regression
* support vector machine
* neural net classifier 들

> 보통 sparse한 데이터에 대해서 svm
dense한 데이터에 대해 nn classifier 가 좋음

## 분류한 단어를 평가
* accuracy
* f1 score

---

## Word2Vec
비슷한 문장 구조에 쓰이는 단어는 비슷할 것이다 <br>  
discrete한 개념인 단어를 수치적인 백터로 바꿔준다. <br>
뺄셈을 통해 유클리드 공간에서 위치백터를 만들어낸다.   
> 작은 벡터에 정보를 우겨 넣어야하며 back propagation 같은 연산을 통해 이루어지는 최신 최적화 기법을 적용하려면 벡터간의 거리가 미분가능한, 이산적이지 않은 개념으로 정의되어야한다.

> man:woman 과 king:queen 의 반의어 관계에서, f(man) - f(woman) 이 f(king) - f(queen) 의 유사함을 얻을 수 있고
f(king) - f(man) + f(woman)으로 queen 을 유추할 수 있다.<br>

>의마가 비슷하다는 의미와 관계의 정의에 대한 개념이 들어감

<img src="https://scontent.ficn2-1.fna.fbcdn.net/v/t1.0-9/40854067_1108342015997309_3433158060535709696_n.png?_nc_cat=104&oh=69e498b3d56691b40a493af0c54524a5&oe=5C5D2E52"/>


* skip gram
CBOW 보다 좀 더 성능이 좋음 <br>
* CBOW
center word를 추론하는 CBOW

### Word similarity task

### 활용
* GloVe
* fastText

---

## Images and Words

### CNN (Convolutional Neural Network)
word2vec 을 통해 만든 수치 데이터 (저차원)과 시너지

<img src="https://scontent.ficn2-1.fna.fbcdn.net/v/t1.0-9/41792862_1113713542126823_7762157977309544448_o.png?_nc_cat=108&oh=a86c788d22d6363049da62a11025eaaa&oe=5C4E66B3"/>


## 단어
* discrete(이산) : 불연속적인 수치
* distributional semantics(분산) : 비슷한 context에 등장하는 녀석들은 실제로도 비슷한/관련 있는 녀석들일 가능성이 높다
* sparse
* precision : 1이라고 했을 때 정말 맞을 확률  
* recall : 맞은 것들 중 1이라고 했을 확률

## See alse
* [썰로 풀어보는 NLP](https://www.facebook.com/pg/nobodybelongs/notes/)
