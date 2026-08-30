---
title: "Trace"
permalink: /portfolio/trace/
layout: single
author_profile: true
toc: true
toc_sticky: true
comments: false
share: false
---

<div class="portfolio-hero">
  <p class="portfolio-kicker">Workflow Automation, Field Operations</p>
  <h1>Trace</h1>
  <p class="portfolio-lead">
    별도 장비관리 UI를 새로 도입하지 않고 Slack 대화에서 장비 등록, 이동, 반입, 반출, 상태 변경, 추적, 이력을 처리하고 Google Sheets에 master와 audit log를 유지하는 경량 장비 추적 시스템입니다.
  </p>
  <div class="portfolio-actions">
    <a class="portfolio-action" href="https://github.com/shaunsukgyukoh/Trace-testflight">GitHub Repository</a>
  </div>
</div>

<div class="portfolio-facts">
  <div class="portfolio-fact"><strong>Slack First</strong><span>Existing workflow as the user interface</span></div>
  <div class="portfolio-fact"><strong>Audit Trail</strong><span>Append-only movement history</span></div>
  <div class="portfolio-fact"><strong>AI Parsing</strong><span>Gemini natural-language intent extraction</span></div>
  <div class="portfolio-fact"><strong>Low Infra</strong><span>Apps Script and Google Sheets backend</span></div>
</div>

## 문제 정의

의료기기와 demo 장비는 병원, 대리점, 전시회, 본사, 해외 국가 사이를 반복적으로 이동합니다.

Spreadsheet를 사람이 직접 수정하는 방식에서는 다음 문제가 발생할 수 있습니다.

- 실제 장비 위치와 sheet 정보 불일치
- serial 표기 방식 차이로 검색 누락
- 이동 과정에서 과거 상태와 위치가 덮어써짐
- 별도 asset management UI 접속으로 입력 friction 증가
- duplicate serial 등록
- 상태, 위치, 담당자 명칭의 표기 흔들림
- 누가 언제 무엇을 변경했는지 추적하기 어려움

<div class="portfolio-callout">
<strong>핵심 문제 재정의</strong><br>
새로운 장비관리 화면을 추가하기보다 기존 Slack workflow 안에서 입력을 끝내고, backend가 data integrity와 history를 자동으로 보장하도록 했습니다.
</div>

## 해결 방안

### Slack as Interface

Slack message를 Events API로 받고 Google Apps Script Web App에서 처리합니다.

지원 workflow는 등록, 추적, 이력, 상태변경, 반입, 반출, 이동입니다.

### Natural-language Parsing

정해진 command뿐 아니라 자연어 문장을 Gemini가 intent와 field로 구조화할 수 있도록 구성했습니다.

### Single Source of Truth

Google Sheets를 세 역할로 분리했습니다.

~~~text
EquipmentMaster
  -> Current equipment state

MovementLog
  -> Append-only history

ErrorLog
  -> Event and backend error trace
~~~

### Serial Integrity

full serial uppercase normalization, duplicate block, exact match 우선, abbreviated serial search를 구현했습니다.

### Canonical Normalization

병원명, 대리점명, 국가명 표현이 달라도 alias rule을 통해 canonical value로 정리합니다.

### Deterministic Business Rules

AI가 intent와 field를 추출하더라도 duplicate check, allowed status, serial validation, normalization은 deterministic rule로 처리합니다.

## 이해관계자와 요구사항 반영

주요 사용자는 장비를 실제 이동시키는 field-service와 운영 담당자입니다.

새로운 application을 학습하게 하는 대신 기존 Slack에서 업무를 끝낼 수 있도록 했고, 운영 관점에서는 입력 편의뿐 아니라 serial integrity, 상태 검증, 변경 이력 보존을 함께 반영했습니다.

또한 별도 server나 상용 asset-management SaaS를 추가하지 않고 기존 Slack과 Google Workspace 자원을 활용하는 low-infrastructure architecture를 선택했습니다.

## 본인 기여

- Slack Events API, Apps Script Web App architecture 설계
- EquipmentMaster, MovementLog, ErrorLog data model 설계
- 등록, 추적, 이력, 상태변경, 이동 workflow 구현
- duplicate serial validation 구현
- full serial, abbreviated serial search 구현
- country, location, delivery partner lookup 구현
- alias normalization rule 구현
- serial prefix 기반 model mapping 구현
- allowed status, usage validation 구현
- 변경 전후 위치와 operator append-only log 구현
- Slack thread reply feedback 구현
- Gemini natural-language parsing, business rule flow 구성
- ErrorLog, Slack error response failure handling 구현

## 최종 결과와 성과

<ul class="portfolio-result-list">
  <li>장비관리 action을 별도 UI 없이 Slack conversation에서 처리하는 workflow를 구현했습니다.</li>
  <li>current state와 historical log를 분리해 최신 정보와 audit trail을 동시에 유지합니다.</li>
  <li>duplicate serial registration을 차단해 master data integrity를 강화했습니다.</li>
  <li>full serial을 몰라도 abbreviated serial, 국가, 위치, 담당자로 equipment lookup이 가능합니다.</li>
  <li>canonical normalization을 통해 표기 차이에 따른 검색 누락을 줄일 수 있는 구조를 마련했습니다.</li>
  <li>자연어 입력을 structured update로 변환하는 AI-assisted workflow를 구축했습니다.</li>
</ul>

## 인사이트와 러닝

### 내부 도구는 기존 workflow 안에 들어갈 때 adoption이 쉬워집니다

사용자가 이미 Slack을 사용하고 있다면 새로운 management UI보다 Slack을 command surface로 사용하는 편이 입력 friction을 줄일 수 있습니다.

### Current state와 history는 분리해야 합니다

최신 상태 table과 append-only event log를 분리하면 operational convenience와 auditability를 함께 확보할 수 있습니다.

### AI parsing 뒤에도 deterministic rule이 필요합니다

AI output을 바로 database write로 연결하지 않고 serial validation, allowed state, duplicate check, canonical normalization을 deterministic layer로 유지하는 것이 안정성에 중요했습니다.

## 기술 스택

<div class="portfolio-tags">
<span class="portfolio-tag">Slack API</span>
<span class="portfolio-tag">Google Apps Script</span>
<span class="portfolio-tag">Google Sheets</span>
<span class="portfolio-tag">Gemini API</span>
<span class="portfolio-tag">JavaScript</span>
</div>

## 한계와 확장

Apps Script quota와 execution limit이 있어 높은 event volume에서는 queue와 별도 backend가 필요합니다. 향후 request signature verification, authorization, approval flow, dashboard, periodic inventory report를 추가할 수 있습니다.
