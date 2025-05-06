# 🏗️ 시스템 설계: {{기능 이름}} (예: 경매 입찰 처리)

---

## 🎯 요구사항
- 실시간 입찰 요청 처리
- 동시성 보장
- 낙찰 결과 정산

---

## 🧱 아키텍처 구성

```mermaid
graph TD
Client --> API
API --> Kafka
Kafka --> BidProcessor
BidProcessor --> DB
