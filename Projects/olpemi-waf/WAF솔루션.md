### 주요 기능

#### 🔍 WAF 기능 확장
- [[WAF 확장 - 딥웹 탐지 로직 추가]]

#### 📈 모니터링 대시보드
- [[모니터링 대시보드 - WAF 탐지 현황]]
- 모니터링 대시보드 - 매트릭(tps, mbps)

그 외
- 성능 추적
- 빌드 배포 프로세스


## ✅ MVP

>**최소 기능 제품(Minimum Viable Product, MVP)**

#### WAF 솔루션
- 딥웹 탐지
- Ruleset 기반 요청 필터링
#### 모니터링 웹
- 탐지 현황 모니터링
- 시스템 메트릭 모니터링
- Ruleset 관리
- 딥웹 솔루션 관리
- Ruleset, 딥웹 변경사항 적용


딥웹 정보 업데이트
- 관리자 페이지에서 크롤러 관리(수동 실행, 자동 실행 주기 관리)
- 딥웹 크롤러 → MySQL 저장되는 형태

MySQL to Config, Nginx reload
이벤트 발생 : 1. 모니터링 웹에서 RuleSet 변경 시 2. 딥웹 정보 업데이트 시

메트릭 정보 수집
프로메테우스를 이용한 시스템 메트릭 정보 수집