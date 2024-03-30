---
sticker: emoji//1f929
---
# 모던 프론트엔드 개발자가 꼭 알아야할 서버리스 서비스들

### Modern Web Application
CSR -> SSR -> Micro Architect

### 서버리스란?
관리가 필요없다. 
유연성
고가용성
불필요한 지출 방지

### Amplify
AWS 아키텍트에게 함 물어봐야겠땅

Amplify studio

### Labmda
Cold Start, Warm Start -> Snapshot Caching(자바만 가능)

5분마다 헬스체크


### gateway

service discovery -> msa 환경에서 유용

## SAM 도와줘요! 로컬에서 람다를 테스트 해볼 수 있을까?

Sam (IaC) -> CloudFormation을 활용하여 서버리스 애플리케이션을 관리


SAM - Gateway 
LocalStack - S3 
로컬에서 대체하여 테스트

LocalStack

RIE
RIC

람다를 도커로


## 부하 테스트

로드 테스팅
높은 부하가 걸려있는 상태로 기능을 검증

스트레스 테스트

스파이크 테스트

Soak Testing

서버리스에서 부하 테스트를 하는 이유
1. 비용을 미리 파악할 수 있습니다. - 견적내기 까다로움
2. 서비스 할당량의 추가 요청을 위한 근거 수집 - AWS를 포함, 클라우드 서비스에는 사용할 수 있는 할당량이 존재합니다. 
3. 최적화와 성능 튜닝 - 람다의 실행에도 다양한 설정이 존재하기 때문에 부하 테스트 결과를 보는 것이 좋음

람다의 버스트 동시성, 일반적인 동시 실행 수는 별개로 고려해야합니다. 


