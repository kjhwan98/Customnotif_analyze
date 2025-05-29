# Customnotif_analyze
## 업데이트 중

### 파일 설명
데이터가 프라이빗해서 전처리된 파일과 코드를 일부만 공개
<br/> 시각화 -> 결과 시각화: 전처리된 csv 파일로 핵심 결과 시각화
<br/> 전처리 -> 알림 전처리: 핵심 전처리 과정
<br/> 전처리 -> Fire to csv: 파이어베이스에서 수집되는 데이터 연동

### 실험자 모집
<img src=https://github.com/user-attachments/assets/43ae269c-bc85-48b5-aa17-9c81ffd2ae96 width="500" height="800"/>

### 로그 수집 데이터 설명
| 컬럼명                 | 설명                                                                 |
|------------------------|----------------------------------------------------------------------|
| `deviceId`             | 사용자별 개별 디바이스 ID (랜덤 지정)                                 |
| `eventType`            | 사용자의 휴대폰 사용 로그 (화면 On/Off, 알림 수신, 상단바 확인 등)    |
| `isCharging`           | 충전 중인지 여부                                                      |
| `package_name`         | 앱 패키지명 (앱 이름)                                                |
| `ringerMode`           | 알림 모드 (무음, 진동, 소리)                                         |
| `timestamp`            | 이벤트 발생 시간                                                     |
| `className`            | 앱 내 클래스명 (사용하지 않음)                                       |
| `action`               | 앱 사용 행동 (아이템 제거, 추가, 요청 버튼 클릭 등)                  |
| `importanceLevel`      | 설정한 알림 수신 모드 (즉시받기 / 사용중 받기 / 요청시 받기)         |
| `itemName`             | 설정한 아이템의 이름 (앱 이름, 키워드 내용)                          |
| `itemType`             | 설정한 아이템의 유형 (앱 / 키워드)                                   |
| `pendingNotificationCount` | 알림 요청 버튼 클릭 시 쌓여 있던 알림 수                              |
| `notification_id`      | 알림 ID (동일 앱 내 다른 종류의 알림 구분 가능)                      |
| `post_time`            | 알림이 수신된 시간                                                   |
| `text`                 | 알림 텍스트 (프라이버시 보호를 위해 앞뒤 3글자만 남기고 익명화)       |
| `title`                | 알림 제목                                                            |
| `removal_reason`       | 알림 제거 이유 (클릭, 스와이프, 모두 지우기, 자동 취소 등)           |
| `removal_time`         | 알림이 제거된 시간                                                   |

<img src=https://github.com/user-attachments/assets/d4a2aece-55a9-4756-b9e0-b9a34a3eefad width="400" height="500"/>
<br/> 
<br/> 'deviceId': 사용자별 개별 디바이스 ID (랜덤 지정)
<br/> 'eventType': 사용자의 휴대폰 사용 로그 (화면을 키고 끄기, 알림이 옴, 상단바를 내려 알림을 확인 등)
<br/> 'isCharging': 충전 중인지 아닌지
<br/> 'package_name': 앱 패키지명 (앱 이름)
<br/> 'ringerMode': 알림 모드(무음, 진동, 소리)
<br/> 'timestamp': 이벤트 발생 시간
<br/> 'className': 앱 안에서의 클래스 (필요 없음)
<br/> 'action': 앱 사용 행동(아이템을 제거했는지, 추가했는지, 요청 버튼을 눌렀는지)
<br/> 'importanceLevel': 설정한 알림 수신 모드 (즉시받기/사용중 받기/요청시 받기)
<br/> 'itemName': 설정한 아이템의 이름(앱 이름, 키워드 내용)
<br/> 'itemType': 설정한 아이템이 앱인지 키워드인지 
<br/> 'pendingNotificationCount': 사용자가 알림 요청 버튼을 눌렀을 때 몇개가 쌓여있는지
<br/> 'notification_id' : 알림 ID (같은 앱에서 온 알림이어도 종류가 다름) ex. 토스앱에서 만보기 알림, 송금 알림 등 분류 가능
<br/> 'post_time': 알림이 온 시간
<br/> 'text' : 알림 텍스트 (프라이버시를 위하여, 앞뒤 3글자만 남기고 익명화(*)
<br/> 'title' : 알림 제목
<br/> 'removal_reason' : 알림이 제거된 이유(클릭, 스와이프, 모두 지우기, 자동 취소 등)
<br/> 'removal_time': 알림이 제거된 시간

### 전처리 앱: 알림이 로그에는 뜨지만, 자동으로 삭제되는 앱(사용자가 인지 못하는 알림)
remove = [ "app.revanced.android.youtube", "com.blizzard.messenger", "com.bodyplusone.android.bodycalendar", "com.cashwalk.cashwalk", "com.fast.free.unblock.thunder.vpn", "com.google.android.apps.maps", "com.google.android.apps.tachyon", "com.google.android.packageinstaller", "com.hanbit.rundayfree", "com.ims.dm", "com.kmusicmp3", "com.microsoft.office.outlook", "com.openai.chatgpt", "com.ovpnspider", "com.samsung.android.app.earphonetypec", "com.samsung.android.app.galaxyregistry", "com.samsung.android.app.telephonyui", "com.samsung.android.audiomirroring", "com.samsung.android.bixby.agent", "com.samsung.android.game.gametools", "com.samsung.android.mdecservice", "com.samsung.android.oneconnect", "com.samsung.android.singletake.service", "com.samsung.android.smartmirroring", "com.samsung.android.themestore", "com.samsung.knox.securefolder", "com.sec.android.app.camera", "com.sec.android.app.myfiles", "com.sec.android.easyMover", "com.sec.android.gallery3d", "com.sec.knox.kccagent", "com.shirokovapp.instasave", "com.surfshark.vpnclient.android", "com.whatsapp", "com.windyty.android", "com.wooriib.pib.smart", "droom.sleepIfUCan", "io.runable.runable", "jp.pokemon.pokemontcgp", "kr.co.lylstudio.httpsguard", "kr.go.mobileid", "us.zoom.videomeetings" ]

### 설문지 리스트 (멘탈 지수 평가)
- 나는 휴대전화가 없으면 공허함을 느낀다
- 나는 휴대전화 사용에 많은 시간을 사용하고 있다
- 나는 휴대전화에 집착하고 있다
- 나는 휴대전화가 없을 때 단절감을 느낀다
- 나는 휴대전화 사용이 금지된 곳에 있으면 불안하다
- 나는 과도한 알림으로 인해 주의가 산만해진적이 있다
- 나는 매일 쏟아지는 알림에 압도당한다고 생각한다
- 나는 알림을 통해 쏟아지는 정보가 너무 많아서 이를 처리하는데 어려움을 느낀다.
- 나는 다른 업무를 하는 동안 다양한 알림을 너무 많이 받는다고 생각한다
- 나는 가끔 알림으로 인해 과부하를 느낀다
- 나는 내가 처리할 수 있는 양보다 더 많은 수의 알림을 받는다
- 알림이 계속 오면 긴장을 풀기 어렵다
- 밀린 알림을 처리한 후에 피곤함을 느낀다
- 알림 처리 때문에 피로감을 느낀다
- 알림을 처리하고 나면, 나만의 여유 시간에 집중하기 어렵다
- 알림을 처리하는 동안, 나는 다른 업무를 제대로 수행할 수 없을 정도로 피곤함을 느낀다.

### 관련 논문 정리
[스프레드시트](https://docs.google.com/spreadsheets/d/1agNk2Z9rJXQGeGbLCixgLzCGnnxc4Rr6/edit?usp=sharing&ouid=113323787086455513564&rtpof=true&sd=true)
