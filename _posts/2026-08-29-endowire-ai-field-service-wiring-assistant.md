---
title: "EndoWire AI, 내시경 AI 시스템 현장 배선 자동 설계 SW"
date: 2026-08-29
categories:
  - Portfolio
tags:
  - Medical AI
  - Field Service
  - JavaScript
  - Workflow Automation
  - Mermaid
toc: true
toc_sticky: true
---

## 프로젝트 한 줄 소개

내시경 시스템의 종류와 모니터 구성, 실제 사용 가능한 포트, 현장 보유 케이블과 컨버터 재고를 입력하면 설치 가능한 배선 연결도와 준비물 목록을 자동 생성하는 필드서비스용 의사결정 지원 소프트웨어입니다.

[실행 데모 바로가기](https://shaunsukgyukoh.github.io/projects/endoscopy-wiring-assistant/)

## 문제 정의

의료기관마다 사용 중인 내시경 프로세서, 모니터, 외부 Gateway의 포트 구성이 다르고 현장에 준비된 케이블, splitter, switch, converter의 종류와 수량도 다릅니다.

AI Processing PC를 추가 설치할 때는 원본 영상 우회 경로, AI 처리 영상, 단일 또는 듀얼 모니터, Gateway 연결을 동시에 고려해야 하므로 숙련자의 경험에 의존하기 쉽습니다.

이 프로젝트는 이러한 현장 노하우를 포트 호환성과 재고 제약조건으로 구조화해, 필드서비스 인원이 높은 수준의 영상 인터페이스 지식이 없어도 설치 구성을 결정할 수 있도록 하는 것을 목표로 했습니다.

## 해결 방식

사용자는 현재 현장에서 직접 확인할 수 있는 조건만 입력합니다.

- 내시경 출력 포트
- AI Processing PC 입력 포트
- 모니터 구성
- 모니터 가용 입력 포트
- Gateway 사용 여부
- 보유 케이블, splitter, switch, converter 수량

애플리케이션은 가능한 연결 경로를 평가하고, 최종적으로 성공한 경로만 Mermaid 연결도와 BOM으로 출력합니다.

## 핵심 기술 아이디어

단순한 고정 배선도 선택이 아니라 작은 constraint-based routing engine으로 구현했습니다.

후보 경로를 시도하기 전에 다음 상태를 snapshot합니다.

- 남은 재고
- 현재 BOM
- 그래프 상태
- 남은 AI Processing PC 출력
- 정의된 graph node

후속 연결에서 실패하면 상태를 rollback하고 다른 경로를 탐색합니다.

이 방식으로 포트가 맞더라도 실제 현장 재고가 없으면 선택되지 않고, 직접 케이블이 없으면 converter fallback 경로를 사용할 수 있습니다.

## 사용자 경험

목표 사용자는 영상 인터페이스 전문가가 아니라 현장 설치 절차를 정확히 따라야 하는 필드서비스 인원입니다.

따라서 복잡한 호환 규칙을 사용자에게 설명하는 대신, 현재 보이는 포트와 수량만 선택하게 하고 결과는 시각적인 연결도와 준비물 체크리스트로 제공합니다.

## 기술 스택

- HTML5
- Vanilla JavaScript
- Tailwind CSS
- Mermaid 10
- Rule-based constraint search
- Browser-only static architecture

## 프로젝트에서 보여주는 역량

이 프로젝트의 핵심은 UI 화면 자체보다 실제 필드서비스 도메인 지식을 재사용 가능한 소프트웨어 규칙으로 전환한 것입니다.

특히 다음 역량을 보여줍니다.

- 현장 문제를 소프트웨어 요구사항으로 구조화
- 복수 제약조건을 고려한 경로 탐색 로직 설계
- 비숙련 사용자 중심의 workflow 단순화
- 시각화와 BOM을 통한 작업 산출물 자동화
- 실제 서비스 플랫폼으로 확장 가능한 rule-engine 관점

## 향후 확장

- 장비 모델별 포트 사양 DB
- JSON 기반 compatibility rule engine
- 자동화된 routing unit test
- 연결 안정성, 변환 횟수, 비용 기반 weighted path optimization
- 병원별 설치 profile 저장
- PDF 설치 작업지시서 자동 생성
- PWA offline mode
- QR 기반 준비물 확인과 설치 완료 기록

## 면접에서 설명하는 방법

> 의료기관마다 내시경, 모니터, Gateway의 포트 구성이 다르고 현장에 가지고 간 케이블과 컨버터도 달라 AI PC 설치가 숙련자의 경험에 의존하는 문제가 있었습니다. 저는 이 노하우를 포트 호환성과 재고 제약조건으로 구조화해, 현장 조건을 선택하면 가능한 배선 경로를 탐색하고 Mermaid 연결도와 BOM을 자동 생성하는 웹 SW를 만들었습니다. 후보 경로가 중간에 실패하면 사용한 재고와 그래프 상태를 rollback한 뒤 다른 경로를 찾도록 구현했습니다. 핵심은 필드서비스 경험을 재사용 가능한 의사결정 소프트웨어로 전환했다는 점입니다.

## 관련 링크

- [Interactive Demo](https://shaunsukgyukoh.github.io/projects/endoscopy-wiring-assistant/)
- [Project README](https://github.com/shaunsukgyukoh/shaunsukgyukoh.github.com/blob/main/projects/endoscopy-wiring-assistant/README.md)
- [Architecture](https://github.com/shaunsukgyukoh/shaunsukgyukoh.github.com/blob/main/projects/endoscopy-wiring-assistant/ARCHITECTURE.md)
- [Test Scenarios](https://github.com/shaunsukgyukoh/shaunsukgyukoh.github.com/blob/main/projects/endoscopy-wiring-assistant/TEST_SCENARIOS.md)
- [Interview Notes](https://github.com/shaunsukgyukoh/shaunsukgyukoh.github.com/blob/main/projects/endoscopy-wiring-assistant/INTERVIEW_NOTES.md)
