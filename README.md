# ⚡ CastPro 매뉴얼

캐스트프로 전기차 충전기 · 서버 연동 및 운영 매뉴얼입니다.

## 📚 서버

충전기와 서버 간 통신 명세입니다.

### OCPP 1.6

- [OCPP 메시지 명세](server/ocpp/messages.md) 👉 Authorize | BootNotification | StartTransaction | StopTransaction | MeterValues | StatusNotification | Heartbeat | UpdateFirmware | FirmwareStatusNotification | 필수·선택 파라미터
- [OCPP 프로세스 정의](server/ocpp/process.md) 👉 회원 충전 | 비회원 충전 | 충전기 설치 | 펌웨어 업데이트 | 충전기 진단

### REST API

- [결제 REST API](server/rest-api/payment.md) 👉 단가정보 수신 | 결제/취소 결과 전송
- [충전이력 등록 REST API](server/rest-api/charge-history.md)
- [환경부 충전내역 REST API](server/rest-api/env-charge-history.md) 👉 충전내역 등록 | 삭제
- [카드 인증(회원구분 조회) REST API](server/rest-api/card-auth.md) 👉 회원 카드 | 환경부 카드

## 🔌 충전기

현장 설치 · 유지보수용 가이드입니다.

- [충전기 네트워크 설정](charger/network-setup.md) 👉 관리자 메뉴 | 서버 URL·충전소 ID | IP 설정
- [충전기 USB 앱 업데이트](charger/usb-app-update.md) 👉 USB로 APK 업데이트

## 🖥️ 로컬 서버

인터넷 연결 없이 현장 로컬 서버로 운영하는 경우의 가이드입니다.

- [로컬 서버 대시보드 사용 매뉴얼](local-server/dashboard.md) 👉 로그인 | 대시보드 | 충전소·충전기 관리 | 사용·고장 이력 | 매출현황 | 회원 관리
- [로컬 서버용 충전기 설정](local-server/charger-setup.md) 👉 고정 IP 설정 | 펌웨어 초기 설정

## ☸️ 대시보드 운영 (HelloCharger Dashboard)

- [로얄캐닌 포인트 충전 설치 가이드](dashboard/royalcanin-point-charging.md) 👉 회원 추가 | 충전 단가 설정 | 충전기 설정 | 회원별 사용 이력

## 📮 문의

캐스트프로 · rnd@castpro.kr
