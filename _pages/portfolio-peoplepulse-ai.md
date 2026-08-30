---
title: "PeoplePulse AI"
permalink: /portfolio/peoplepulse-ai/
layout: single
author_profile: true
toc: true
toc_sticky: true
comments: false
share: false
---

<div class="portfolio-hero">
  <p class="portfolio-kicker">Data, ML, Responsible AI</p>
  <h1>PeoplePulse AI</h1>
  <p class="portfolio-lead">
    Realtime workplace NLP, monthly activity pipeline, temporal ML, MLOps, local Analyst Agent를 통합하면서 개인정보와 인사 의사결정 경계를 architecture에 포함한 privacy-aware People Analytics 플랫폼입니다.
  </p>
  <div class="portfolio-actions">
    <a class="portfolio-action" href="https://github.com/shaunsukgyukoh/peoplepulse-ai">GitHub Repository</a>
    <a class="portfolio-action" href="https://github.com/shaunsukgyukoh/peoplepulse-ai/tree/portfolio">Portfolio Branch</a>
  </div>
</div>

<div class="portfolio-facts">
  <div class="portfolio-fact"><strong>0.799</strong><span>KLUE RoBERTa Macro-F1, synthetic benchmark</span></div>
  <div class="portfolio-fact"><strong>0.6988</strong><span>ROC-AUC, synthetic attrition reference</span></div>
  <div class="portfolio-fact"><strong>650 x 36</strong><span>Synthetic employees by monthly panel</span></div>
  <div class="portfolio-fact"><strong>36 Cases</strong><span>Deterministic Agent evaluation set</span></div>
</div>

## 문제 정의

조직 데이터를 활용해 업무 부담과 이탈 위험을 분석하는 시스템은 기술적으로 구현 가능하지만 잘못 설계하면 직원 감시 시스템이 될 수 있습니다.

핵심 문제는 다음과 같았습니다.

- Slack raw message 장기 저장에 따른 개인정보 노출 위험
- 직원 단위 심리 상태 추정에 따른 profiling 위험
- realtime communication과 monthly report identity 연결
- 낮은 positive rate와 class imbalance
- random split에 따른 temporal leakage
- model output과 실제 HR decision의 경계
- LLM Agent의 raw employee data와 arbitrary SQL 접근 위험
- experiment, drift, API health를 동시에 운영해야 하는 복잡성

<div class="portfolio-callout">
<strong>핵심 문제 재정의</strong><br>
이탈 가능성이 높은 개인을 찾아내는 모델이 아니라, 데이터 최소화와 정책 경계를 시스템 구조에 포함한 People Analytics platform을 목표로 했습니다.
</div>

## 해결 방안

### Realtime Slack Pipeline

Slack Events API와 Socket Mode로 message event를 받고 PII masking과 HMAC pseudonymization 후 Redis Streams로 전달합니다.

raw message를 analytics database에 장기 보관하지 않고 NLP derived signal만 저장하도록 했습니다.

### Monthly Data Pipeline

서로 다른 monthly report format을 parser가 자동 인식하고 Pandera validation과 privacy filter를 거쳐 monthly feature로 변환합니다.

### Feature Store

Slack과 monthly report identifier를 동일한 HMAC namespace로 연결하고 PostgreSQL에 rolling feature를 저장합니다.

### Temporal ML

7일, 30일, 90일 rolling feature와 trend delta를 만들고 future target window와 purge gap을 포함한 temporal split을 적용했습니다.

### Responsible Agent

LangGraph, Ollama Agent에 arbitrary SQL을 제공하지 않고 fixed read-only tool만 허용했습니다. LLM 앞의 deterministic policy gate가 individual real-employee risk, raw content, employment decision, mental-health inference를 차단합니다.

### MLOps

MLflow experiment tracking, Evidently drift, Prometheus metrics, Grafana dashboard를 Docker Compose stack으로 통합했습니다.

## 이해관계자 관점과 협업

개인 portfolio project로 진행했기 때문에 실제 HR 조직이나 직원 데이터를 사용한 공동 개발은 하지 않았습니다.

대신 requirements를 다음 stakeholder 관점으로 분리했습니다.

- HR 운영자, 조직 단위 workload trend와 report 상태
- 직원, raw communication과 개인 정보 보호
- Data/ML engineer, 재현 가능한 feature와 evaluation
- 운영자, drift와 service monitoring
- Analyst Agent 사용자, 근거가 있는 read-only analytics

서로 충돌하는 요구를 architecture boundary와 policy로 명시했습니다.

## 본인 기여

- Slack realtime ingestion, Redis Streams pipeline 설계
- PII masking, HMAC pseudonymization 구현
- KLUE RoBERTa 기반 Korean workplace multi-label NLP 구축
- monthly report ingestion, Pandera validation 구현
- identity resolution, PostgreSQL feature store 구축
- rolling feature, temporal target pipeline 구현
- Logistic Regression, XGBoost, LightGBM, CatBoost 비교
- probability calibration, SHAP 적용
- FastAPI backend, Next.js dashboard, SSE 구현
- MLflow, Evidently, Prometheus, Grafana 통합
- LangGraph, Ollama local Analyst Agent 구현
- deterministic privacy guard, evaluation harness 구현
- synthetic와 real-data scope를 분리하는 branch strategy 설계

## 최종 결과와 성과

### NLP Benchmark, Synthetic Portfolio Dataset

| Model | Macro-F1 | Macro Precision | Macro Recall | P95 Latency |
|---|---:|---:|---:|---:|
| KLUE RoBERTa-base | **0.799** | 0.732 | 0.969 | 7.26 ms |
| TF-IDF + Logistic | 0.557 | 0.593 | 0.767 | **2.61 ms** |
| KcELECTRA-base | 0.476 | 0.353 | 0.948 | 6.66 ms |
| KcELECTRA-small | 0.263 | 0.158 | 0.917 | 7.81 ms |

### Synthetic Attrition Reference

- Average Precision, **0.1238**
- ROC-AUC, **0.6988**
- Recall@Top10%, **0.2683**
- Calibrated Brier Score, **0.0566**
- Test Positive Rate, **5.76%**

employee-level ML은 synthetic data에만 적용했습니다.

### Agent Evaluation

single-tool, multi-tool, source trace, privacy attack를 포함한 36개 deterministic case를 구성하고 tool selection, citation, unsupported numeric claim, latency를 함께 평가하는 harness를 구현했습니다.

## 인사이트와 러닝

### Responsible AI는 문서가 아니라 architecture constraint여야 합니다

raw message 비저장, pseudonymization, aggregate-only real analytics, read-only tool, policy gate처럼 위험한 행동을 구조적으로 하기 어렵게 만드는 설계가 중요했습니다.

### 불균형 문제에서는 accuracy가 핵심 metric이 아닙니다

낮은 positive rate에서는 AP, Recall@Top-K, calibration을 함께 확인해야 실제 screening 성능을 이해할 수 있었습니다.

### ML output과 product decision은 분리해야 합니다

모델 결과는 분석 신호일 뿐 인사 의사결정 자체가 아닙니다. 특히 employment domain에서는 model performance와 허용되는 decision scope를 별도로 정의해야 했습니다.

## 기술 스택

<div class="portfolio-tags">
<span class="portfolio-tag">Python</span>
<span class="portfolio-tag">PyTorch</span>
<span class="portfolio-tag">Transformers</span>
<span class="portfolio-tag">KLUE RoBERTa</span>
<span class="portfolio-tag">Redis</span>
<span class="portfolio-tag">PostgreSQL</span>
<span class="portfolio-tag">Pandera</span>
<span class="portfolio-tag">XGBoost</span>
<span class="portfolio-tag">LightGBM</span>
<span class="portfolio-tag">SHAP</span>
<span class="portfolio-tag">FastAPI</span>
<span class="portfolio-tag">Next.js</span>
<span class="portfolio-tag">MLflow</span>
<span class="portfolio-tag">Evidently</span>
<span class="portfolio-tag">LangGraph</span>
<span class="portfolio-tag">Ollama</span>
</div>

## 한계

- employee-level model 결과는 synthetic data에만 해당합니다.
- causal attrition prediction을 주장하지 않습니다.
- protected-class fairness evaluation은 공개 dataset에 demographic label을 포함하지 않아 수행하지 않았습니다.
- Docker Compose는 single-machine reproducible environment이며 HA production infrastructure는 아닙니다.
