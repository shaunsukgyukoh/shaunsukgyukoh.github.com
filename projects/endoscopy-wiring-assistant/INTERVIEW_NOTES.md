# Interview Notes

## Resume bullet

Designed and implemented a browser-based field-service wiring decision tool that converts heterogeneous endoscopy, AI-PC, monitor, Gateway, and accessory inventory constraints into a validated wiring topology and BOM using rule-based route search with rollback.

## Korean resume bullet

내시경, AI PC, 모니터, Gateway의 가용 포트와 현장 자재 재고를 제약조건으로 모델링하고, 후보 경로 실패 시 상태를 rollback하며 설치 가능한 배선도와 BOM을 자동 생성하는 필드서비스 의사결정 SW 설계 및 구현.

## STAR

**Situation**

Installation conditions differed by medical site and depended heavily on experienced engineers.

**Task**

Reduce preparation omissions and make wiring decisions understandable for less-experienced field staff.

**Action**

Converted field rules into port and inventory constraints, implemented candidate routing with rollback, visualized the validated topology with Mermaid, and generated a quantity-based preparation checklist.

**Result**

Created a repeatable workflow that can standardize installation reasoning and can be extended into a model-specific rule engine and service platform.

## Why not a static wiring manual?

A static manual works only when equipment combinations are fixed. The actual problem changes with endoscopy output, monitor inputs, AI-PC input, Gateway use, and the accessories physically available at the site. This tool therefore treats installation as a constraint-satisfaction problem.

## Why rollback?

A locally valid connection can consume an accessory that makes the full topology impossible later. Snapshot and rollback prevent a failed candidate from contaminating the next routing attempt.
