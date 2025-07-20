# 🎵 Real-Time Mood-Based Music Recommendation with EEG Emotion Recognition

> **EEG 기반 실시간 감정 인식 + 음악 추천 시스템**
> 사용자의 실시간 감정 상태를 배우고 그에 맞는 음악을 추천하는 엔드투엔드 프레임워크 구축

---

## 📌 프로젝트 개요

* **기존 음악 추천 시스템의 한계**: 클릭 로그, 재생 이력 등 간적 정보 기반 → 사용자 감정 상태 반영 없음
* **해결 방안**: 실시간 EEG 기반 감정 인식 → Valence-Arousal 모델을 통해 감정 분석 후 음악 추천
* **활용 복잡**: 심리 안정, 감정 조절, 음악 치리 등

---

## 🧠 시스템 구성도

```
EEG (DEAP) ▶ Mood Regressor ▶ Predicted Emotion (Valence/Arousal)
                                     │
           Music DB (DEAM+FMA) ────────┛
                         │
       ▶ Cosine Similarity Matching
                         ▼
              🎵 최종 추천 음악 리스트
```

---

## 🧪 사용 데이터 및 모델

### 📊 DEAP Dataset (EEG 기반 감정 래이블)

* 32명, 40개의 1분 길이 음악 영상
* 감정 지표: Valence, Arousal, Dominance, Liking (1–9점)
* EEG: 32채널, 128Hz, 4초 단위 세부화

### 🎵 DEAM + FMA Dataset (음악 감정 데이터)

* DEAM: 1802개 음악에 Valence/Arousal 래이블 존재
* FMA: DEAM 모델을 통해 FMA 음원에 AV 값 추련해서 감정 태깅

---

## 🔎 감정 인식 모델

### 🤩 CNN 기반 회귀 모델

```
입력: EEG 신호 (4초 단위 세그먼트)
▶ Conv Layer
▶ ReLU + BatchNorm
▶ Fully Connected Layer
▶ Output: Valence & Arousal 값 (0~1 범위)
```

* 정량적 회귀를 통해 감정 상태를 예측 (분류 기능 X)

---

## 🎼 음악 추천 알고리즘

* **Step 1**: EEG로부터 Valence/Arousal 예측
* **Step 2**: 음악 데이터베이스의 AV값과 비교
* **Step 3**: **Cosine Similarity**를 통해 가장 가치가 빠가운 곡 추천

```math
Similarity = cos(θ) = (V₁⋅V₂) / (||V₁|| * ||V₂||)
```

> 🌟 유사도가 \ 놓을수록 감정과 음악 간 일치도가 큼

---

## 🌐 웹 서비스 데모

### 전체 흉법:

1. 사용자 EEG 침시 시작
2. 실시간 감정 예측 (Regression)
3. 음악 추천 결과 실시간 표시
4. 감정 흉법과 음악의 연동 상태 시각화

<details>
<summary>🖼️ Demo 화면 이미지 (추후 이미지 삽입 위치)</summary>

![demo.gif](./images/demo.gif)

</details>

---

## ✅ 프로젝트 결과 요약

* EEG 기반 Valence-Arousal 회귀 모델 구현
* FMA 음악에 감정 래이블 부여 → 감정 유사도 기반 추천
* 실시간 감정 변화에 맞는 음악 추천 가능
* 사용자 감정 공감과 안정 효과 기능

---

## 🔮 한우 확장 방향

* 🤍 Dominance 값 포함한 3차원 감정 베터 활용
* 🎵 감정 맞춤 → 감정 조절로 시스템 확장
* 📋 플레이리스트 단위 최적화
* 📷 멀티모달 입력: 아이 트래킹, 아티워 표정 등 각호
* 🧬 정신 건강 관리/치리 도구로 응용 가능

---

## 📚 참고 문헌

1. **Koelstra et al., 2011** - DEAP: A Database for Emotion Analysis using Physiological Signals
2. **Javidan et al., 2021** - Regression-based Emotion Recognition with Two EEG Channels
3. **Liu et al., 2020** - Multi-level Features Guided Capsule Network
4. **Sampaio et al., 2022** - Facial Expression Algorithms in Interactive Media

---

## 📁 프로젝트 구성 예시

```
📆 mood-music-recommender
├── README.md
├── /models
│   └── mood_regressor_cnn.pth
├── /data
│   ├── deap/
│   ├── deam/
│   └── fma/
├── /scripts
│   ├── regression_model.py
│   └── recommender.py
├── /images
│   └── demo.gif
└── /webapp
    ├── app.py
    └── templates/
```

---

> Ⓒ DL Team 6 | 2025 | Real-Time Emotion-Aware Music Recommendation Framework
