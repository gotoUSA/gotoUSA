Python 백엔드 신입 개발자입니다. Django/DRF와 Celery로 결제, 인증, 비동기 처리가 있는 쇼핑몰 REST API를 만들었고, 외부 API 장애에 대응하는 Python 라이브러리를 설계해 PyPI에 출시했습니다. 쇼핑몰은 Kubernetes에 배포해 장애 시험을 했고, 라이브러리 공개 문서로 RAG를 만들어 답변 검증과 검색 평가를 했고, 공개 데이터로 품질 검사와 분석도 해 봤습니다. 오픈소스 rq, InvenTree, django-payments에 버그 수정 PR 4건이 머지됐습니다.

아래 프로젝트는 모두 Claude로 개발했습니다. AI로 작성한 코드와 결과는 테스트 통과만으로 판단하지 않고, 공식 문서, 실제 API 호출, 다시 계산한 숫자와 대조합니다. 쇼핑몰, Kubernetes, RAG, Olist 저장소에는 제가 직접 정한 것과 AI에 맡긴 것을 나눠 적었습니다.

## 프로젝트

- [Django 쇼핑몰 REST API](https://github.com/gotoUSA/selfhealing): 동시 주문과 중복 결제 방지, 상품 목록 쿼리 수정으로 요청 1.3초 → 36ms, 로컬 부하 테스트(동시 요청 10개, 10분) p95 6.1초 → 170ms, p99 6.9초 → 280ms
- [쇼핑몰 Kubernetes 배포](https://github.com/gotoUSA/shopping-k8s): 로컬 클러스터 배포, 무중단 교체(교체 중 연결 실패 7건 → 0건), 자동 확장(HPA), Helm 전환과 장애 시험 기록
- [Baldur](https://github.com/baldurhq/baldur): Python 외부 API 장애 대응 라이브러리
- [Baldur 문서 RAG](https://github.com/gotoUSA/baldur-docs-rag): Baldur 공개 문서 질의응답, 모델의 인용 번호와 Tool Calling 인자를 코드로 검증하고 질문 세트 3개로 검색 품질 측정
- [Olist 데이터 품질 검사와 분석](https://github.com/gotoUSA/olist-data-quality): 공개 주문 데이터 약 10만 건, 검사 기준을 먼저 정하고 자동 검사와 오류 주입 테스트를 만든 뒤 배송 지연과 리뷰 점수의 관계 분석

## 오픈소스 기여 (머지됨)

- [rq #2526](https://github.com/rq/rq/pull/2526): Redis가 응답하지 않으면 워커가 종료 코드 0으로 꺼져 자동 재시작되지 않던 문제
- [InvenTree #12990](https://github.com/inventree/InvenTree/pull/12990): Slack 알림 HTTP 호출에 timeout 추가
- [django-payments #501](https://github.com/jazzband/django-payments/pull/501): stripe 15 이상 지원
- [django-payments #510](https://github.com/jazzband/django-payments/pull/510): 같은 웹훅이 다시 와도 결제를 한 번만 확정

## 글

- [AI가 작성한 코드를 실제 환경에서 검증하고 고친 기록](https://github.com/gotoUSA/gotoUSA/blob/main/docs/ai-code-verification.ko.md): AI로 작성한 코드에서 찾은 결함(결제사에 없는 서명을 검증하던 웹훅, mock 서버에서만 통과한 기능 등)과 그 뒤 바꾼 개발 방식
