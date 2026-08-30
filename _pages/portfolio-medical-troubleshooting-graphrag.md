---
title: "Medical Device Troubleshooting GraphRAG"
permalink: /portfolio/medical-troubleshooting-graphrag/
layout: single
author_profile: true
toc: true
toc_sticky: true
comments: false
share: false
---

<div class="portfolio-hero">
  <p class="portfolio-kicker">GraphRAG, Medical Device AI</p>
  <h1>Medical Device Troubleshooting GraphRAG</h1>
  <p class="portfolio-lead">
    의료기기 유지보수 매뉴얼과 Trouble Report에 흩어진 지식을 Symptom, Cause, Solution, Verification 관계로 구조화하고, Hybrid Retrieval, Knowledge Graph, Reranker, evidence guardrail을 결합한 필드서비스 troubleshooting 지원 시스템입니다.
  </p>
  <div class="portfolio-actions">
    <a class="portfolio-action" href="https://github.com/shaunsukgyukoh/medical-troubleshooting-graphrag">GitHub Repository</a>
  </div>
</div>

<div class="portfolio-facts">
  <div class="portfolio-fact"><strong>Hybrid RAG</strong><span>BGE-M3, BM25, RRF</span></div>
  <div class="portfolio-fact"><strong>Knowledge Graph</strong><span>Neo4j relationship expansion</span></div>
  <div class="portfolio-fact"><strong>Human Review</strong><span>Candidate knowledge approval gate</span></div>
  <div class="portfolio-fact"><strong>Safe Failure</strong><span>Escalation and abstention</span></div>
</div>

## 문제 정의

필드서비스 엔지니어는 반복적으로 유사한 장애를 해결하지만 장애 원인과 해결 이력은 유지보수 매뉴얼, 사내 문서, 과거 Trouble Report에 분산됩니다.

Vector RAG만으로는 다음 문제가 남았습니다.

- symptom과 의미적으로 가까운 문서는 찾지만 cause, solution, verification 관계를 명시적으로 활용하기 어려움
- 기술 용어 exact match와 자연어 paraphrase에 강한 검색 방식이 서로 다름
- LLM이 source에 없는 해결 절차를 생성할 위험
- verified solution이 없는 문제에도 강제로 답변할 위험
- answer가 어떤 evidence를 근거로 생성되었는지 추적해야 함
- 과거 report에는 성공한 해결뿐 아니라 실패한 시도도 포함됨

<div class="portfolio-callout">
<strong>핵심 문제 재정의</strong><br>
답변 coverage를 높이는 RAG보다, 검증된 근거가 없으면 해결책을 생성하지 않는 troubleshooting knowledge system을 목표로 했습니다.
</div>

## 해결 방안

### Structured Knowledge

TroubleCase를 Pydantic schema와 Markdown/YAML Wiki로 구조화했습니다.

~~~text
Symptom
  -> Cause
  -> Solution
  -> Verification
~~~

### Hybrid Retrieval

BGE-M3, Qdrant Dense Retrieval과 BM25 Sparse Retrieval을 구축하고 Reciprocal Rank Fusion으로 결과를 결합했습니다.

### Knowledge Graph

Ollama와 qwen3:8b로 entity와 relation candidate를 추출하고 normalization, deduplication 후 Neo4j graph로 구조화했습니다.

### Human Review Gate

LLM extraction 결과를 canonical knowledge로 바로 사용하지 않고 validation, normalization, human approval 단계를 거치도록 했습니다.

### GraphRAG and Reranker

Hybrid retrieval 결과를 graph seed로 사용해 related evidence를 확장하고 BGE cross-encoder reranker로 final relevance를 다시 평가합니다.

### Answer Guardrail

verified solution evidence가 없으면 해결책을 만들지 않고 escalation 또는 abstention 상태를 반환하도록 설계했습니다.

## 이해관계자와 협업

개인 engineering project로 구현해 별도 개발팀과 공동 개발하지는 않았습니다.

다만 실제 필드서비스 지식 운영을 기준으로 요구사항을 세 관점으로 분리했습니다.

- 필드서비스 엔지니어, 빠른 symptom 검색과 실행 가능한 근거 필요
- 지식 관리자, LLM extraction의 review와 승인 필요
- 품질 관점, 잘못된 solution과 failed attempt의 재추천 방지 필요

이 요구를 retrieval, knowledge review, answer safety layer로 분리했습니다.

## 본인 기여

- TroubleCase schema와 Knowledge Wiki 설계
- BGE-M3, Qdrant Dense Retrieval 구축
- BM25와 RRF Hybrid Retrieval 구현
- Neo4j graph schema 설계
- Ollama structured extraction pipeline 구현
- entity normalization, deduplication 구현
- Human Review Gate와 approval workflow 구현
- graph expansion과 BGE reranker 적용
- grounded generation과 citation validation 구현
- verified solution, escalation, abstention guardrail 구현
- FastAPI backend, Streamlit UI 구현
- Docker Compose full stack 구성
- historical trouble report sanitization, candidate review flow 설계
- retrieval, answer safety benchmark framework 구축

## 최종 결과와 성과

<ul class="portfolio-result-list">
  <li>Dense, Sparse, Hybrid, Graph, Reranker를 하나의 retrieval pipeline에서 비교 가능한 구조로 만들었습니다.</li>
  <li>Troubleshooting knowledge를 explicit relationship graph로 모델링해 downstream Cause, Solution, Verification evidence를 탐색할 수 있도록 했습니다.</li>
  <li>LLM extraction을 자동 정답으로 사용하지 않고 review queue를 거쳐 canonical knowledge로 승격하도록 구현했습니다.</li>
  <li>승인된 TroubleCase만 Qdrant와 Neo4j에 incremental publish하는 Knowledge Management workflow를 구축했습니다.</li>
  <li>historical trouble record 21건을 review candidate catalog로 구성하고 failed attempt를 negative evidence로 보존하는 구조를 마련했습니다.</li>
  <li>FastAPI, Streamlit, Qdrant, Neo4j를 Docker Compose로 통합해 재현 가능한 local environment를 구성했습니다.</li>
</ul>

현재 공개 benchmark result table은 evaluation framework만 준비되어 있고 측정값이 채워지지 않은 상태이므로 성능 수치를 성과로 제시하지 않았습니다.

## 인사이트와 러닝

### Troubleshooting은 document retrieval보다 relationship retrieval에 가깝습니다

사용자는 symptom을 입력하지만 실제로 필요한 정보는 cause, solution, verification으로 이어지는 관계입니다. 이 특성 때문에 Vector Retrieval과 Graph Traversal을 결합하는 구조가 적합했습니다.

### LLM extraction과 knowledge approval은 분리해야 합니다

형식적으로 올바른 structured output이 실제 현장 지식으로 검증되었다는 뜻은 아닙니다. candidate와 canonical knowledge의 lifecycle을 분리하는 것이 중요했습니다.

### failed attempt도 중요한 지식입니다

실패한 해결 절차를 삭제하는 대신 negative evidence로 보존하면 같은 잘못된 action이 다시 추천되는 위험을 줄일 수 있습니다.

## 기술 스택

<div class="portfolio-tags">
<span class="portfolio-tag">Python</span>
<span class="portfolio-tag">Pydantic</span>
<span class="portfolio-tag">BGE-M3</span>
<span class="portfolio-tag">Qdrant</span>
<span class="portfolio-tag">BM25</span>
<span class="portfolio-tag">Neo4j</span>
<span class="portfolio-tag">BGE Reranker</span>
<span class="portfolio-tag">Ollama</span>
<span class="portfolio-tag">FastAPI</span>
<span class="portfolio-tag">Streamlit</span>
<span class="portfolio-tag">Docker Compose</span>
</div>

## 한계

- 공개 dataset은 synthetic 또는 anonymized된 소규모 데이터입니다.
- 최종 retrieval benchmark 수치는 아직 publish되지 않았습니다.
- graph schema는 의료기기 troubleshooting에 특화되어 있습니다.
- public production deployment에는 authentication, TLS, rate limiting, audit logging이 추가로 필요합니다.
