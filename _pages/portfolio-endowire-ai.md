---
title: "EndoWire AI"
permalink: /portfolio/endowire-ai/
layout: single
author_profile: true
toc: true
toc_sticky: true
comments: false
share: false
---

<div class="portfolio-hero">
  <p class="portfolio-kicker">Field Service Automation, Decision Support</p>
  <h1>EndoWire AI</h1>
  <p class="portfolio-lead">
    내시경, AI Processing PC, 모니터, Gateway의 가용 포트와 현장 보유 케이블, splitter, switch, converter 재고를 입력하면 설치 가능한 배선 경로와 준비물 목록을 자동 생성하는 필드서비스 의사결정 지원 소프트웨어입니다.
  </p>
  <div class="portfolio-actions">
    <a class="portfolio-action" href="https://github.com/shaunsukgyukoh/EndoWire_AI">GitHub Repository</a>
    <a class="portfolio-action" href="https://shaunsukgyukoh.github.io/EndoWire_AI/">Live Demo</a>
  </div>
</div>

<div class="portfolio-facts">
  <div class="portfolio-fact"><strong>5 Interfaces</strong><span>HDMI, DVI, SDI, DP, YPbPr routing</span></div>
  <div class="portfolio-fact"><strong>Inventory Aware</strong><span>Available cable and converter quantities</span></div>
  <div class="portfolio-fact"><strong>Rollback</strong><span>Failed candidate state recovery</span></div>
  <div class="portfolio-fact"><strong>BOM Output</strong><span>Validated route material checklist</span></div>
</div>

## 문제 정의

의료기관마다 사용하는 내시경 프로세서와 모니터의 영상 포트가 다르고, AI Processing PC 설치에 사용할 수 있는 케이블과 변환 장비도 현장마다 다릅니다.

실제 설치에서는 다음 조건을 동시에 고려해야 합니다.

- 내시경 출력과 AI PC 입력 호환성
- 단일 또는 듀얼 모니터 구성
- AI 영상과 원본 영상의 동시 제공
- 원본 영상 fail-safe bypass
- Gateway 사용 여부
- 보유 케이블, splitter, switch, converter 수량

이 판단이 숙련자의 경험에 의존하면 준비물 누락, 잘못된 케이블 준비, 현장 재작업 가능성이 커집니다.

<div class="portfolio-callout">
<strong>핵심 문제 재정의</strong><br>
배선도를 문서로 많이 만드는 것이 아니라, 현장 조건을 제약조건으로 입력하면 전체 topology가 성립하는 설치안을 계산하도록 했습니다.
</div>

## 해결 방안

사용자가 현장에서 직접 확인할 수 있는 포트와 자재 수량만 선택하면 내부 routing logic이 가능한 설치 경로를 평가합니다.

1. raw video distribution용 splitter 후보 선택
2. interface가 다를 경우 converter fallback 탐색
3. AI Processing PC input route 구성
4. monitor configuration에 따라 AI와 raw route 배정
5. Gateway 사용 시 남은 output과 inventory로 추가 route 계산
6. 최종 valid route의 자재만 BOM으로 집계
7. Mermaid diagram과 checklist 생성

### Constraint-based Routing

후보 연결을 시도하기 전에 inventory, BOM, graph state, 남은 AI PC output을 snapshot합니다.

후속 연결에서 전체 topology가 실패하면 이전 상태로 rollback하고 다른 후보를 평가합니다.

~~~text
Site Conditions
  -> Port Constraints
  -> Inventory Constraints
  -> Candidate Route
  -> Full Topology Validation
       -> Fail, Rollback and Retry
       -> Success, Diagram and BOM
~~~

## 이해관계자와 요구사항 반영

실제 사용자군을 설치 경험 수준이 서로 다른 field-service 인력으로 정의했습니다.

복잡한 영상 interface 지식을 입력하도록 요구하지 않고 장비 뒤에서 직접 확인할 수 있는 port와 material quantity만 입력하도록 UI를 단순화했습니다.

또한 AI 영상 연결만 성공하는 것이 아니라 원본 영상 bypass를 유지해야 하는 운영 요구를 routing 조건에 포함했습니다.

## 본인 기여

- 실제 설치 업무를 port, material, output resource constraint로 모델링
- HDMI, DVI, SDI, DP, YPbPr 연결 rule 구현
- direct cable이 없을 때 converter chain fallback 구현
- candidate failure 시 inventory, BOM, graph state rollback 구현
- single monitor fail-safe, dual monitor, Gateway route 구현
- Mermaid 기반 실시간 wiring diagram 생성
- 최종 material 자동 집계 BOM 구현
- impossible configuration failure handling 구현

## 최종 결과와 성과

<ul class="portfolio-result-list">
  <li>브라우저에서 별도 server 없이 실행되는 interactive installation tool을 구현했습니다.</li>
  <li>port와 inventory가 변경되면 wiring diagram과 BOM을 실시간 재계산합니다.</li>
  <li>single monitor, dual monitor, Gateway configuration을 하나의 UI에서 처리합니다.</li>
  <li>자재 부족이나 interface incompatibility가 있으면 잘못된 설치안을 제시하지 않고 failure state를 명확하게 표시합니다.</li>
  <li>현장 엔지니어의 설치 판단을 반복 사용할 수 있는 routing rule로 전환했습니다.</li>
</ul>

## 인사이트와 러닝

### 현장 지식은 문장보다 constraint로 구조화할 때 재사용성이 높습니다

장비 조합별 manual page를 늘리는 방식보다 port compatibility와 material consumption rule을 분리하면 새로운 장비를 추가할 때 기존 engine을 재사용할 수 있습니다.

### local success와 global success는 다릅니다

앞 단계 연결이 성공해도 뒤에서 필요한 cable이나 converter가 부족할 수 있습니다. 전체 topology validation과 rollback이 필요한 이유였습니다.

### 결과의 설명 가능성이 현장 실행력을 높입니다

가능 여부만 보여주는 것보다 실제 연결도와 준비물 목록을 함께 제시해야 사용자가 결과를 검증하고 실행할 수 있습니다.

## 기술 스택

<div class="portfolio-tags">
<span class="portfolio-tag">HTML5</span>
<span class="portfolio-tag">JavaScript</span>
<span class="portfolio-tag">Tailwind CSS</span>
<span class="portfolio-tag">Mermaid</span>
<span class="portfolio-tag">Constraint Routing</span>
<span class="portfolio-tag">Rule Engine</span>
</div>

## 한계와 확장

실제 의료기관 설치에서는 제조사 공식 manual과 현장 SOP를 최종 기준으로 검증해야 합니다.

향후 장비 model별 port DB, JSON rule externalization, weighted graph search, automated routing test, PDF work order, offline PWA로 확장할 수 있습니다.
