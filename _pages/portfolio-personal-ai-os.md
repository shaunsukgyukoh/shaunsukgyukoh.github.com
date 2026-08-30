---
title: "Personal AI OS"
permalink: /portfolio/personal-ai-os/
layout: single
author_profile: true
toc: true
toc_sticky: true
comments: false
share: false
---

<div class="portfolio-hero">
  <p class="portfolio-kicker">Agentic AI, Local AI Platform</p>
  <h1>Personal AI OS</h1>
  <p class="portfolio-lead">
    반복적인 개인 업무와 정보 모니터링을 로컬 AI가 처리할 수 있도록, Ollama, LangGraph, n8n, PostgreSQL/pgvector, MCP, automation registry를 통합한 self-hosted AI agent platform입니다.
  </p>
  <div class="portfolio-actions">
    <a class="portfolio-action" href="https://github.com/shaunsukgyukoh/personal-ai-os">GitHub Repository</a>
  </div>
</div>

<div class="portfolio-facts">
  <div class="portfolio-fact"><strong>Jetson AGX Orin</strong><span>Local inference and orchestration environment</span></div>
  <div class="portfolio-fact"><strong>MCP Tool Layer</strong><span>Memory, automation, integration contract</span></div>
  <div class="portfolio-fact"><strong>Persistent Memory</strong><span>PostgreSQL and pgvector semantic memory</span></div>
  <div class="portfolio-fact"><strong>Safety First</strong><span>Approval-gated high-risk automation</span></div>
</div>

## 문제 정의

이메일, 일정, 채용 공고, 국가 지원 과제, 금융 정보, 기술 뉴스처럼 반복적으로 확인해야 하는 업무가 여러 서비스에 흩어져 있으면 사용자는 매번 앱을 열고 검색하고 정리해야 합니다.

단순 chatbot만으로는 실제 자동화 시스템에 필요한 다음 조건을 해결하기 어렵습니다.

- 여러 도구와 외부 서비스를 일관된 방식으로 연결
- 반복 작업을 미래 시점에 실행하는 scheduler
- 이전 작업과 사용자 정보를 유지하는 persistent memory
- 동일 자동화의 중복 등록 방지
- 외부 상태를 변경하는 action에 대한 승인 정책
- 실패 task의 상태와 재시도 가능성 추적
- cloud API 의존도를 줄인 local-first 실행 환경

<div class="portfolio-callout">
<strong>핵심 문제 재정의</strong><br>
LLM이 대답하는 비서가 아니라, 상태, 기억, 도구, 예약 실행, 안전 정책을 지속적으로 관리하는 개인용 AI 운영 기반이 필요했습니다.
</div>

## 해결 방안

기능을 하나의 거대한 Agent에 넣지 않고 책임별 layer로 분리했습니다.

~~~text
User
  -> Hermes Agent
  -> FastAPI Orchestrator
      -> LangGraph Routing
      -> Automation Planner
      -> Safety Policy
      -> MCP Tool Layer
      -> Memory Service
  -> PostgreSQL / pgvector
  -> Ollama
  -> n8n and Integrations
~~~

### Orchestrator

사용자 요청을 route별 workflow로 분기하고 LangGraph state transition과 local LLM을 연결했습니다.

### Memory Service

텍스트 memory를 embedding하고 PostgreSQL/pgvector에 저장해 semantic search가 가능하도록 별도 service로 분리했습니다.

### Automation Registry

cron, one-time task를 database에 등록하고 next run time, enabled state, failure count, last result, last error를 추적합니다.

동일 요청이 반복되는 문제를 줄이기 위해 action, schedule, timezone을 바탕으로 dedupe key를 생성합니다.

### Safety Layer

외부 상태를 변경하는 high-risk action은 즉시 실행하지 않고 approval state로 이동할 수 있도록 설계했습니다.

## 이해관계자와 협업

개인 프로젝트로 진행해 외부 개발팀과의 공동 개발은 없습니다.

대신 여러 open-source component를 하나의 product architecture로 통합하는 과정에서 각 도구의 책임 경계를 명확히 했습니다.

- Hermes Agent, 사용자 interface
- LangGraph, routing과 state transition
- n8n, workflow automation
- MCP, tool contract
- PostgreSQL/pgvector, durable state와 memory
- Ollama, local inference
- FastAPI, service boundary

## 본인 기여

- Jetson AGX Orin 기반 local AI runtime 구축
- Ollama local inference 연결
- FastAPI orchestrator와 LangGraph routing 구현
- PostgreSQL/pgvector memory service 구현
- memory save/search MCP tool 구현
- automation create/list/status tool layer 구현
- cron, one-time automation task registry 구현
- idempotent dedupe key와 task lifecycle 설계
- due task claim, success, failure state 처리 구현
- risk classification과 approval-gated safety policy 구현
- Docker Compose 기반 PostgreSQL, n8n, service stack 구성
- secrets와 runtime configuration 분리

## 최종 결과와 성과

<ul class="portfolio-result-list">
  <li>Orchestrator, Memory Service, MCP Tool Layer, Automation Registry를 독립 component로 구현했습니다.</li>
  <li>cron과 one-time schedule, 중복 방지, due task claim, 실행 결과와 실패 상태 기록을 database 기반으로 처리했습니다.</li>
  <li>semantic memory를 local database에 저장하고 Agent가 MCP를 통해 검색할 수 있는 구조를 구축했습니다.</li>
  <li>고위험 automation을 approval state로 전환하는 safety boundary를 설계했습니다.</li>
  <li>개별 자동화 script보다 공통 memory, scheduling, safety, tool contract를 우선 구축해 이후 domain agent를 같은 구조 위에 추가할 수 있게 했습니다.</li>
</ul>

## 인사이트와 러닝

### Agent 시스템의 핵심은 LLM보다 상태 관리에 가깝습니다

실제 자동화에서는 답변 생성보다 task가 이미 등록되었는지, 실행 중인지, 실패했는지, 재시도 가능한지 관리하는 것이 중요했습니다. Agentic system에는 model integration뿐 아니라 workflow engine과 database design이 필요했습니다.

### autonomy보다 control boundary가 먼저입니다

모든 action을 동일한 권한으로 실행하는 방식보다 읽기, 예약, 외부 변경 action을 분리하고 승인 상태를 명시하는 구조가 장기적으로 안전하고 확장성이 높았습니다.

### Local-first 환경은 resource-aware engineering을 요구합니다

Jetson에서는 model size, context, container resource, storage, inference latency를 같은 하드웨어 안에서 함께 고려해야 했습니다.

## 기술 스택

<div class="portfolio-tags">
<span class="portfolio-tag">Python</span>
<span class="portfolio-tag">FastAPI</span>
<span class="portfolio-tag">LangGraph</span>
<span class="portfolio-tag">Hermes Agent</span>
<span class="portfolio-tag">Ollama</span>
<span class="portfolio-tag">n8n</span>
<span class="portfolio-tag">PostgreSQL</span>
<span class="portfolio-tag">pgvector</span>
<span class="portfolio-tag">MCP</span>
<span class="portfolio-tag">Docker Compose</span>
</div>

## 현재 범위와 다음 단계

Core orchestration, memory, MCP tool, automation safety layer까지 구현되어 있으며 email/calendar, job monitoring, grant monitoring, finance, search/browser, content automation을 동일 contract 위에서 확장하는 구조입니다.
