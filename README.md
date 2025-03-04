# 🚨 응급상황 자동 인식 및 응급실 연계 서비스

<div align="center">
  <img src="https://github.com/user-attachments/assets/put-your-image-id-here" alt="응급상황 서비스 로고" width="500px" />
  <br><br>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white" />
  <img src="https://img.shields.io/badge/Transformers-FF6F00?style=for-the-badge&logo=huggingface&logoColor=white" />
  <img src="https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white" />
  <img src="https://img.shields.io/badge/NAVER_Maps-03C75A?style=for-the-badge&logo=naver&logoColor=white" />
  <br><br>
  <p><i>KT AIVLE School AI 트랙 미니프로젝트 6차</i></p>
</div>

<br>

## 📋 프로젝트 개요

<div align="center">
  <h3><i>"응급상황 음성인식부터 응급실 연계까지의 통합 서비스 구축"</i></h3>
</div>

<br>

본 프로젝트는 응급 상황에서 환자의 생명을 구하기 위한 핵심 요소인 '빠른 판단'과 '신속한 이송'을 지원하는 AI 기반 서비스를 개발하는 것을 목표로 합니다. 응급 전화를 통해 접수된 상황을 자동으로 인식하고, 응급 등급을 분류한 후, 환자와 가까운 적절한 응급실을 추천하는 통합 파이프라인을 구축했습니다.

<br>

## ⏰ 프로젝트 기간
- 2025년 3월 — 2025년 3월 (4일간)

<br>

## 📝 문제 정의

```
❓ 응급상황에서 환자의 생명을 살리는 데에 가장 중요한 요소는 무엇일까?
```

<br>

### 응급 상황의 현실적 문제점:

- 🔹 **응급실 상황 확인에 시간 소요**: 병실 여유가 있는 응급실을 찾는데 시간이 지체됨
- 🔹 **제한된 응급실 자원**: 응급실 병상은 항상 부족한 상황
- 🔹 **응급 환자 분류의 어려움**: 실제 응급환자가 아닌 경우에도 응급실에 입원하는 사례가 많음
- 🔹 **중증 응급환자 적정 치료 저해**: 국회 보건복지위원회 자료에 따르면, 2020년부터 2023년까지 4년간 응급실 내원 환자 중 준응급 및 비응급(4, 5등급) 환자의 비율이 평균 53.3%로 절반 이상을 차지
- 🔹 **경증 환자 응급실 과밀화**: 2020년~2024년 7월까지 응급실에 내원한 4, 5등급 환자의 주요 진단명은 감염성 위장염 및 대장염(78만여 건), 복부 및 골반 통증(73만여 건), 손목 및 손의 열린 상처(68만여 건) 등 비응급 사례가 다수

<div align="center">
  <img src="https://github.com/user-attachments/assets/put-emergency-stats-image-id-here" alt="응급실 내원 환자 중증도 분류 통계" width="600px" />
</div>

<br>

### 응급 상황 자동 인식이 중요한 이유:

- 🔹 **빠른 판단**: 응급 상황의 신속한 인식과 중증도 분류
- 🔹 **신속한 이송**: 환자 상태와 위치에 맞는 최적의 응급실로 빠르게 이송
- 🔹 **자원의 효율적 분배**: 응급 등급에 따른 의료 자원의 효율적 활용
- 🔹 **최적 경로 선택**: 교통 상황을 고려한 최적의 응급실 추천

<br>

## 🔍 시스템 구성

본 프로젝트는 다음과 같은 3단계 절차로 구성되어 있습니다:

<div align="center">
  <img src="https://github.com/user-attachments/assets/put-system-architecture-image-id-here" alt="시스템 구성도" width="800px" />
</div>

1. **음성 인식 및 요약(1단계)**: 응급 전화 음성을 텍스트로 변환하고 핵심 정보 요약
2. **응급 상황 등급 분류(2단계)**: 요약된 텍스트를 바탕으로 응급 등급(1~5) 분류
3. **응급실 연계/추천(3단계)**: 응급 등급, 교통 상황, 응급실 위치를 고려한 최적 응급실 추천

<br>

## 🏥 한국 응급환자 중증도 분류 기준 (KTAS)

응급환자의 중증도 분류를 위해 한국 응급환자 중증도 분류기준(Korean Triage and Acuity Scale, KTAS)을 활용하였습니다. 이 기준은 보건복지부고시(제2023-287호, 2023.12.28. 시행 2024.1.1)에 의해 규정되어 있습니다.

### 중증도 등급 분류

| 등급 | 분류 | 상태 | 대응 필요성 |
|-----|-----|------|------------|
| 1등급 | 소생 | 생명이나 사지가 위험한 상태 | 즉시 처치 필요 |
| 2등급 | 긴급 | 생명이나 사지가 위험할 가능성이 있는 상태 | 매우 긴급한 처치 필요 |
| 3등급 | 응급 | 응급 처치가 필요하나 생명이나 사지 위험이 낮은 상태 | 긴급 처치 필요 |
| 4등급 | 준응급 | 환자 상태가 안정적이며 응급으로 치료할 필요가 낮은 상태 | 비교적 빠른 처치 필요 |
| 5등급 | 비응급 | 경증 질환 상태 | 긴급하지 않은 처치 가능 |

### 환자 분류

- **중증 응급환자**: 중증도 분류결과 1등급(소생) 및 2등급(긴급)
- **중증 응급의심환자**: 중증도 분류결과 3등급(응급)
- **경증 응급환자 및 비응급환자**: 중증도 분류결과 4등급(준응급) 및 5등급(비응급)

**현황**: 국립중앙의료원이 제출한 자료에 따르면, 2020년~2023년 응급실 내원 환자 중 준응급/비응급 환자(4, 5등급)는 평균 53.3%로 나타남
- 2020년: 55.0%
- 2021년: 53.0%
- 2022년: 53.4%
- 2023년: 51.8%(잠정치)

<div align="center">
  <img src="https://github.com/user-attachments/assets/put-ktas-image-id-here" alt="응급실 내원 환자 분류 기준" width="600px" />
</div>

<br>

## 🛠️ 활용 모델 및 API

### 1. OpenAI Whisper
- **역할**: 음성 인식(STT)
- **특징**: 
  - 680,000시간 분량의 다국어 데이터 기반으로 훈련된 자동 음성 인식(ASR) 시스템
  - 인코더-디코더 트랜스포머 구조
  - 입력 오디오는 30초 청크로 분할되어 log-Mel 스펙트로그램으로 변환

### 2. OpenAI GPT-3.5-turbo
- **역할**: 텍스트 요약 및 키워드 추출
- **특징**:
  - 자연어 이해 및 생성 능력
  - 16K 컨텍스트 창 지원
  - 빠른 응답 시간과 낮은 대기 시간

### 3. KLUE/BERT-base
- **역할**: 한국어 응급상황 텍스트 분류
- **특징**:
  - 한국어 NLP 작업을 위해 사전 학습된 BERT 모델
  - KAIST와 네이버 AI Lab의 연구팀이 주도한 KLUE 프로젝트의 일환
  - Bidirectional(양방향) 문맥 이해 능력
  - 12개 레이어, 768 Hidden Size, 12 Attention Heads, 약 110M 파라미터

### 4. NAVER Maps API
- **역할**: 실시간 도로 거리 및 소요시간 계산
- **특징**:
  - 네이버 클라우드 플랫폼에서 제공하는 지도 API
  - Direction 5 서비스 활용 (자동차 이동 거리 서비스)
  - 실시간 교통 상황을 반영한 이동 시간 계산

### 5. 공공데이터 포털 API
- **역할**: 전국 응급의료기관 정보 수집
- **특징**:
  - 국립중앙의료원에서 제공하는 전국 응급의료기관 정보 조회 서비스
  - 데이터 구성: 기관명, 주소, 응급의료기관분류, 전화번호, 좌표(위도, 경도)
  - 실시간 응급실 현황 정보 확인 가능

<br>

## 🧠 데이터셋

### 1. 응급상황 음성 데이터
- 제공된 응급상황 샘플 음성 파일 5개
- 직접 녹음한 응급 등급별 음성 데이터 (1~5등급 각 2개 이상)
- 총 15개 이상의 테스트용 음성 파일 구축

### 2. 응급 등급 분류 학습 데이터
- 한국 응급환자 중증도 분류기준(KTAS) 기반 데이터셋
- 등급별 최소 100건씩, 총 500건 이상의 텍스트 데이터
- 데이터 형태: (응급상황 텍스트, 응급등급)
- 중증도 카테고리별 샘플 데이터 활용

### 3. 응급실 정보 데이터
- 전국 응급의료기관 정보 조회 서비스 API 활용
- 약 500여 개의 전국 응급실 정보 데이터베이스 구축
- 데이터 구성: 기관명, 주소, 응급의료기관분류, 전화번호, 좌표(위도, 경도)

<br>

## 📊 모델링 결과

### BERT 모델 파인튜닝 결과
- 학습 데이터: 등급별 100건 이상, 총 500건 이상
- 하이퍼파라미터:
  - Learning rate: 1e-5
  - Batch size: 32
  - Epochs: 10
  - Weight decay: 0.02
- 모델 성능: 
  - 정확도(Accuracy): 0.95 이상
  - 각 등급별 정밀도(Precision) 및 재현율(Recall): 0.90 이상
- 혼동 행렬(Confusion Matrix) 분석 결과:
  - 1~5등급 분류에서 높은 정확도 달성
  - 특히 1~3등급(응급 상황)과 4~5등급(비응급 상황) 구분에서 우수한 성능

<div align="center">
  <img src="https://github.com/user-attachments/assets/put-confusion-matrix-image-id-here" alt="BERT 모델 혼동 행렬" width="500px" />
</div>

<br>

## 🧪 활용 예시 및 결과

### 응급 상황 시나리오 테스트 (준응급 사례)
```
<신고전화>
"119죠. 제가 지금 집에 왔는데요. 
댁 도착했는 38도 정도 돼요. 
머리가 아프고 좀 힘한 것 같아요. 
오한이 좀 들어요. 어떻게 해야 할까요?"

<음성 인식 및 요약>
"열이 올라 38도, 머리 아프고 어지러움, 의식 뚜렷"

<분류된 응급 등급>
4등급 (준응급 상황)

<응급실 추천 결과>
"응급상황이 아닌 것으로 판단됩니다. 증상이 악화된다면 응급실로 이동하세요"

1. 의료법인인성의료재단상지의원: 거리 2.21km, 소요시간 7.21분
2. 강원특별자치도보건소의원: 거리 2.77km, 소요시간 7.26분 
3. 연세대학교부속세브란스기독병원: 거리 2.92km, 소요시간 9.51분
```

### 응급 상황 시나리오 테스트 (중증 응급 사례)
```
<신고전화>
"안녕하세요, 119 긴급상황이에요. 지금 제 아버지가 갑자기 가슴을 부여잡고 통증을 호소하시면서 
식은땀을 흘리고 계세요. 안색도 창백해지고 숨쉬기도 힘들어하세요. 빨리 도와주세요."

<음성 인식 및 요약>
"심장 통증, 식은땀, 창백한 안색, 호흡곤란"

<분류된 응급 등급>
1등급 (소생 단계 - 가장 위급한 상황)

<응급실 추천 결과>
"응급상황인 것으로 판단됩니다. 즉시 응급실로 이동하세요"

1. A응급의료센터: 거리 3.2km, 소요시간 7분
2. B대학병원 응급실: 거리 4.5km, 소요시간 11분
3. C의료원 응급실: 거리 5.8km, 소요시간 15분
```

### 응급상황 판단 기준
- **1~3등급 판정 시**: 응급상황인 것으로 판단하여 응급실로 이동 권고
- **4~5등급 판정 시**: 응급상황이 아닌 것으로 판단하며, 증상 악화 시 응급실 이동 권고 또는 일반 의료기관 방문 권장

<br>

## 💻 기술 스택

<div align="center">
  <table>
    <tr>
      <th colspan="2" align="center">분류</th>
      <th align="center">기술</th>
      <th align="center">용도</th>
    </tr>
    <tr>
      <td rowspan="3" width="10%">💻</td>
      <td width="20%"><b>언어</b></td>
      <td width="25%">Python</td>
      <td width="45%">전체 프로젝트 개발</td>
    </tr>
    <tr>
      <td><b>데이터 처리</b></td>
      <td>Pandas, NumPy</td>
      <td>데이터프레임 조작 및 전처리</td>
    </tr>
    <tr>
      <td><b>시각화</b></td>
      <td>Matplotlib, Seaborn</td>
      <td>데이터 시각화 및 결과 표현</td>
    </tr>
    <tr>
      <td rowspan="5">🤖</td>
      <td rowspan="2"><b>API</b></td>
      <td>OpenAI API</td>
      <td>음성 인식(Whisper) 및 텍스트 요약(GPT)</td>
    </tr>
    <tr>
      <td>NAVER Maps API</td>
      <td>도로 거리 및 소요 시간 계산</td>
    </tr>
    <tr>
      <td rowspan="3"><b>모델링</b></td>
      <td>Transformers</td>
      <td>BERT 모델 로딩 및 파인튜닝</td>
    </tr>
    <tr>
      <td>PyTorch</td>
      <td>딥러닝 모델 학습</td>
    </tr>
    <tr>
      <td>Scikit-learn</td>
      <td>데이터 전처리, 모델 평가</td>
    </tr>
  </table>
</div>

<br>

## 📈 향후 개선 방향

1. **모델 성능 향상**
   - 더 다양한 응급상황 데이터 수집을 통한 모델 정확도 개선
   - 응급 등급 판단 정확도를 높이기 위한 모델 최적화

2. **사용자 경험 개선**
   - 웹/모바일 애플리케이션 개발을 통한 서비스 접근성 향상
   - 응급 상황 발생 위치 자동 인식 기능 구현
   - 일반 국민들의 중증도 자가 판단 지원을 위한 직관적인 인터페이스 개발

3. **서비스 확장**
   - 실시간 응급실 병상 정보 연동
   - 다국어 지원을 통한 외국인 대상 서비스 확장
   - 응급 의료진과의 실시간 커뮤니케이션 기능 추가

4. **중증 응급환자 중심의 응급실 연계 고도화**
   - 중증도에 따른 맞춤형 응급실 추천 시스템 개발
   - 경증(4, 5등급) 환자의 경우 응급실 대신 근처 의원, 보건소 등 적절한 의료기관 안내 기능 추가
   - 응급실 과밀화 완화를 위한 정책 연계 시스템 개발

<br>

## 👨‍💻 팀원

<div align="center">
  <table>
    <tr>
      <td align="center"><b>이름1</b></td>
      <td align="center"><b>이름2</b></td>
      <td align="center"><b>이름3</b></td>
      <td align="center"><b>이름4</b></td>
      <td align="center"><b>이름5</b></td>
    </tr>
    <tr>
      <td align="center">음성 인식 모듈 개발</td>
      <td align="center">텍스트 요약 모듈 개발</td>
      <td align="center">BERT 모델 파인튜닝</td>
      <td align="center">응급실 추천 알고리즘 개발</td>
      <td align="center">통합 파이프라인 구축</td>
    </tr>
  </table>
</div>

<br>

---

<div align="center">
  <p>본 프로젝트는 KT AIVLE School AI 트랙 미니프로젝트 6차로 진행되었습니다.</p>
  <p>© 2025 KT AIVLE School 6기 AI 트랙 미니프로젝트</p>
</div>
