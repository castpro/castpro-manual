# 결제 REST API

> 원본: `ocpp_api_rest_api_spec260707.docx` (OCPP 메시지 & REST API 명세)

> **※ 참고**
>
> Base URL: https://castprocsms.kr:3003
>
> 호출 방식: REST (GET / POST)
>
> 응답 포맷: JSON

## 단가정보수신 (요청)

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **단가정보수신 (요청)** | 1 | statId | integer | 충전소ID | REST GET |
|  |  | member\_id | string | 회원사 ID (기본: castpro) |  |
|  |  | clientPriceVersioNo | integer | 충전기가 보유 중인 충전단가 버전번호 (없으면 -1) |  |

**▶ 예제**

```
https://castprocsms.kr:3003/station/queryUnitPriceInfo?statId=CP0001&member_id=castpro&clientPriceVersioNo=-1
```

## 단가정보수신 (응답)

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **단가정보수신 (응답)** | 1 | resultCode | string | 결과코드 (000: 성공, 그 외 에러) |  |
|  |  | resultMessage | string | 결과메시지 |  |
|  | 1 | resultData | array |  |  |
|  | 2 | startTime | string | 시작시간 (00~23) |  |
|  | 2 | endTime | string | 종료시간 (01~24) |  |
|  | 2 | dataType | string | stationPrice: 충전소단가 / defaultPrice: 기본단가 |  |
|  | 2 | unitPriceVersionNo | integer | 충전단가 버전번호 |  |
|  | 2 | castproPrice | string | 헬로우차저 단가 |  |
|  | 2 | otherPrice | string | 비회원 단가 |  |
|  | 2 | envPrice | string | 환경부 단가 |  |
|  | 2 | roamingPrice | string | 로밍 단가 |  |
|  | 2 | lowPrice1~4 | string | 한전 단가 저압 1~4 |  |
|  | 2 | highPrice1~4 | string | 한전 단가 고압 1~4 |  |

**▶ 예제**

```json
{"resultCode":"000","resultMessage":"successful","resultData":[{"dataType":"stationPrice","unitPriceVersionNo":14,"startTime":"00","endTime":"01","castproPrice":"324.4","otherPrice":"300.0","envPrice":"324.4","roamingPrice":"300.0",...}]}
```

## 결제/취소 결과전송 (요청)

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **결제/취소 결과전송 (요청)** | 1 | statId | string | 충전소 ID | REST GET |
|  |  | chargerId | string | 충전기 ID |  |
|  |  | AuthNum | string | 승인번호 |  |
|  |  | Authdate | string | 승인일시 |  |
|  |  | CardName | string | 결제 카드 이름 |  |
|  |  | CardNo | string | 결제 카드 번호 |  |
|  |  | Dpt\_Id | string | 결제 단말기 식별 번호 |  |
|  |  | FranchiseID | string | 가맹점 번호 |  |
|  |  | Wh | string | 사용 Wh |  |
|  |  | Message1 | string | 승인시: 카드종류명 / 거절시: 거절사유 |  |
|  |  | Message2 | string | 승인시: OK / 거절시: 거절사유 |  |
|  |  | PurchaseName | string | 매입사명 |  |
|  |  | Status | string | 승인결과 ("O": 성공, 그 외 실패) |  |
|  |  | Amount | string | 공급금액 |  |
|  |  | TaxAmount | string | 부가세 |  |
|  |  | TotalAmount | string | 결제금액 |  |
|  |  | messageType | string | 메시지 구분 (1: 선결제, 2: 실선결) |  |
|  |  | TransType | string | 트랜잭션 유형 (t1: 결제, u1: 결제취소) |  |
|  |  | userId | string | 회원번호 (고정값: 9001021702170217) |  |
|  |  | idTag | string | OCPP idTag (고정값: 9001021702170217) |  |

**▶ 예제**

```
https://castprocsms.kr:3003/payment/appendPayment?statId=10011&chargerId=01&AuthNum=71578041&Status=O&Amount=100&TotalAmount=100&TransType=t1
```

## 결제/취소 결과전송 (응답)

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **결제/취소 결과전송 (응답)** | 1 | resultCode | string | 결과코드 (000: 성공, 그 외 에러) |  |
|  |  | resultMessage | string | 결과메시지 |  |

**▶ 예제**

```json
{
  "resultCode": "000",
  "resultMessage": "successful"
}
```
