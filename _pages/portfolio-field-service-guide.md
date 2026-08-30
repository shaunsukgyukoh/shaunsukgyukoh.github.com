---
title: "Field Service Guide Platform"
permalink: /portfolio/field-service-guide/
layout: single
author_profile: true
toc: true
toc_sticky: true
comments: false
share: false
---

<div class="portfolio-hero">
  <p class="portfolio-kicker">Flutter, Field Service Platform</p>
  <h1>Field Service Guide Platform</h1>
  <p class="portfolio-lead">
    의료기기 설치, 사용자 교육, 체크리스트, troubleshooting, PDF reporting을 하나의 Flutter application으로 구조화해 자사, 대리점, 병원 현장 인력이 동일한 절차를 따라 작업할 수 있도록 만든 field-service enablement platform입니다.
  </p>
  <div class="portfolio-actions">
    <a class="portfolio-action" href="https://github.com/shaunsukgyukoh/Troubleshooting-testflight">GitHub Repository</a>
  </div>
</div>

<div class="portfolio-facts">
  <div class="portfolio-fact"><strong>Flutter</strong><span>Multi-platform application architecture</span></div>
  <div class="portfolio-fact"><strong>Offline First</strong><span>Hive and local persistent state</span></div>
  <div class="portfolio-fact"><strong>7 Languages</strong><span>Localization-ready content pipeline</span></div>
  <div class="portfolio-fact"><strong>PDF Reporting</strong><span>Printable field workflow output</span></div>
</div>

## 문제 정의

제품 설치, 사용자 교육, 유지보수 업무는 단순히 PDF manual을 전달하는 것으로 해결되지 않았습니다.

현장에서는 다음 문제가 반복됩니다.

- 설치 전 외관, 구성품, accessory 확인 누락
- 설치 순서와 사용자 교육 내용의 혼재
- troubleshooting 지식이 엔지니어 경험과 report에 분산
- 국가와 대리점별 언어 차이로 교육 품질 편차 발생
- 인터넷이 불안정한 현장에서 자료 접근 문제
- checklist 수행 결과와 현장 event 관리의 어려움
- Web, PC, Mobile별 내용을 별도 관리할 때 유지보수 비용 증가

<div class="portfolio-callout">
<strong>핵심 문제 재정의</strong><br>
매뉴얼을 앱에 옮기는 것이 아니라, 현장 업무 절차를 재현 가능한 digital workflow로 표준화하는 것을 목표로 했습니다.
</div>

## 해결 방안

### Content-driven Architecture

설치, 운영, troubleshooting content를 UI에 hard-code하지 않고 JSON data model로 분리했습니다. 동일 renderer를 여러 guide와 language에서 재사용할 수 있도록 설계했습니다.

### Offline-first State

Hive와 SharedPreferences를 사용해 현장 네트워크 상태와 관계없이 checklist와 주요 application state를 유지하도록 했습니다.

### Checklist Workflow

설치 전 점검, 작업 진행, 완료 확인을 persistent checklist로 관리하도록 구현했습니다.

### Troubleshooting Structure

장애 정보를 symptom, cause, solution 중심으로 구조화해 문서 전체를 읽는 대신 필요한 field-service 정보를 빠르게 확인할 수 있도록 했습니다.

### Localization

한국어, 영어, 필리핀어, 몽골어, 베트남어, 태국어, 번체 중국어를 하나의 application 구조에서 지원할 수 있도록 content와 UI localization을 분리했습니다.

### Reporting

현장 확인 내용을 PDF로 생성하고 출력할 수 있도록 reporting flow를 구현했습니다.

## 이해관계자와 협업

사용자 요구를 다음 세 그룹으로 나누어 반영했습니다.

- 자사 field-service 인력
- 해외 대리점 service 인력
- 병원에서 설치와 기본 점검을 수행하는 현장 담당자

제품 이해 수준이 서로 다르기 때문에 전문가 중심 설명을 그대로 노출하기보다 작업 순서, 이미지, checklist 중심으로 정보를 재구성했습니다.

실제 제품 자료와 고객 관련 정보는 application logic과 분리해 배포 대상과 권한에 따라 content를 교체할 수 있도록 했습니다.

## 본인 기여

- Flutter multi-platform architecture 설계
- 설치, 운영, troubleshooting reusable content schema 구성
- Provider state, bootstrap flow 구현
- Hive, SharedPreferences persistent state 구현
- checklist UI, 완료 상태 관리 구현
- device master parsing과 field data logic 구현
- trouble record rendering과 search flow 구현
- PDF export, print workflow 구현
- multi-language content, UI localization 구조 구현
- media asset loading, fallback 처리
- GitLab CI, GitHub Actions build/deploy workflow 구성
- 실제 업무 repository를 공개 가능한 sanitized portfolio snapshot으로 재구성

## 최종 결과와 성과

<ul class="portfolio-result-list">
  <li>설치, 운영, troubleshooting, checklist를 하나의 application workflow로 통합했습니다.</li>
  <li>동일 Flutter codebase에서 Web, Desktop, Mobile로 확장 가능한 구조를 마련했습니다.</li>
  <li>network 연결이 불안정해도 checklist state를 유지하는 local persistence를 구현했습니다.</li>
  <li>7개 언어를 하나의 content pipeline에서 관리할 수 있는 localization 구조를 구성했습니다.</li>
  <li>현장 확인 내용을 PDF로 생성하고 출력하는 reporting 기능을 구현했습니다.</li>
  <li>guide content와 application code를 분리해 제품 내용 변경이 code 변경으로 이어지는 범위를 줄였습니다.</li>
</ul>

## 인사이트와 러닝

### Content-heavy 제품에서는 UI보다 content model이 먼저입니다

가이드가 늘어날수록 화면별 구현보다 공통 schema와 renderer를 정의하는 것이 확장성과 유지보수에 중요했습니다.

### Field-service SW에서는 offline과 recovery가 기본 조건입니다

현장 작업 중 network가 끊기거나 app이 종료될 가능성을 고려해 state persistence를 UX의 일부로 설계했습니다.

### 실무 경험을 공개할 때는 security boundary도 engineering입니다

실제 프로젝트를 portfolio로 공개하기 위해 customer data, media, credential, private history를 제거하고 reusable engineering structure만 남기는 sanitization 과정이 필요했습니다.

## 기술 스택

<div class="portfolio-tags">
<span class="portfolio-tag">Flutter</span>
<span class="portfolio-tag">Dart</span>
<span class="portfolio-tag">Provider</span>
<span class="portfolio-tag">Hive</span>
<span class="portfolio-tag">SharedPreferences</span>
<span class="portfolio-tag">PDF</span>
<span class="portfolio-tag">Printing</span>
<span class="portfolio-tag">GitHub Actions</span>
<span class="portfolio-tag">GitLab CI</span>
</div>

## 공개 범위와 한계

공개 repository는 실제 업무 자료를 제거한 sanitized snapshot입니다. 제품 사진, 고객 정보, training media, internal document 원문은 포함하지 않으며 engineering architecture를 검토하기 위한 공개용 code sample입니다.
