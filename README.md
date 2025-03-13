NTP Monlist Flooding Attack Analyze Report 이글루코퍼레이션 원치현
## 1. 개요
NTP Monlist Flooding Attack(또는 NTP Reflection Attack)은 DDoS(Distributed Denial of Service) 공격의 일종으로, NTP(Network Time Protocol) 서버의 monlist 기능을 악용하여 대량의 트래픽을 발생시키는 공격 방식입니다.

## 2. 공격 원리
NTP 서버에는 monlist(모니터 리스트)라는 기능이 있습니다. 이는 최근 접속한 600개의 클라이언트 리스트를 반환하는 기능입니다.       
공격자는 출발지 IP를 피해자의 IP로 위조하여 monlist 요청을 보냅니다.          
NTP 서버는 요청에 응답하면서 600개 이상의 IP 주소 정보를 포함한 대량의 데이터를 피해자의 IP로 전송합니다.          
적은 요청(수 바이트)로도 몇 백 배 이상의 응답 트래픽을 발생시킬 수 있기 때문에 공격자는 손쉽게 피해 서버를 마비시킬 수 있습니다.          

## 3. 공격 과정      
공격자는 출발지 주소를 피해자의 IP로 위조한 monlist 요청을 여러 NTP 서버에 보냄.       
NTP 서버는 해당 요청을 받고, 수십~수백 배의 응답 트래픽을 피해자의 IP로 전송.        
피해자는 대량의 트래픽을 받아 시스템이 과부하에 걸리거나 네트워크가 마비됨.        
공격자는 여러 개의 NTP 서버를 이용해 공격을 증폭시킴.        

## 4. 공격 특징
트래픽 증폭률이 높음 (최대 556배까지 증가 가능)      
간단한 스크립트로도 공격 가능      
출발지 위조(Spoofing) 가능하여 추적이 어려움      
오래된 NTP 서버가 주요 대상 (최신 NTP에서는 monlist 기능이 비활성화됨)
          
## 5. 방어 방법
✅ NTP 서버 보안 설정 변경

monlist 기능이 있는 ntpdc 대신 ntpq 사용
ntp.conf 설정에서 disable monitor 추가
✅ 방화벽에서 불필요한 NTP 트래픽 차단

UDP 123 포트에서 monlist 요청을 차단
네트워크 레벨에서 Rate Limiting 적용
✅ 업데이트된 NTP 버전 사용

최신 NTP 버전에서는 monlist 기능이 제거됨
가능하면 최신 버전(4.2.7 이상)으로 업그레이드
✅ DDoS 대응 솔루션 활용

클라우드 기반 DDoS 방어 시스템 (Cloudflare, Akamai 등) 사용
ISP와 협력하여 IP Spoofing 방지
🔥 요약
NTP Monlist Flooding Attack은 monlist 기능을 이용한 트래픽 증폭 공격임.
UDP 기반 공격으로 출발지 위조(Spoofing)하여 DDoS 공격에 악용됨.
방어 방법으로는 monlist 비활성화, 방화벽 설정, 최신 버전 업데이트 등이 있음.
