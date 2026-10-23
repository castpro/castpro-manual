# 환경부 충전내역 REST API

> 원본: `ocpp_api_rest_api_spec260707.docx` (OCPP 메시지 & REST API 명세)

> **※ 참고**
>
> Base URL: https://castprocsms.kr:3003
>
> 호출 방식: REST POST (body: JSON)
>
> 결과코드: 000 = 성공, 026 / 100 = 실패
>
> resultData: 환경부 서버로부터 수신한 responseData 포함

## 환경부 충전내역 등록 (요청)

| Message | Depth | Variable | DataType | 설명 |
|---|---|---|---|---|
| **충전내역 등록 (요청)** | 1 | bid | string | 기관ID  예) CP |
|  | 1 | bkey | string | 기관인증키 |
|  | 1 | statId | string | 충전소ID |
|  | 1 | chargerId | string | 충전기ID |
|  | 1 | btid | string | 기관거래ID (OCPP StartTransaction.conf의 transactionId) |
|  | 1 | tbid | string | 회원카드 소속기관ID |
|  | 1 | cardNo | string | 회원카드번호 (신용카드 결제 시 기본값 할당) |
|  | 1 | pow | string | 충전량 [Wh] |
|  | 1 | bprice | string | 충전기관 단가 |
|  | 1 | tbprice | string | 회원카드 소속기관 단가 |
|  | 1 | bmon | string | 충전기관 금액 |
|  | 1 | mon | string | 충전금액 |
|  | 1 | tsdt | string | 충전 시작일시 (YYYYMMDDHHmmSS) |
|  | 1 | tedt | string | 충전 종료일시 (YYYYMMDDHHmmSS) |
|  | 1 | rcvdate | string | 수신일시 (YYYYMMDDHHmmSS) |

**▶ 예제 (POST)**

```
POST https://castprocsms.kr:3003/charge/registerChargeHistory body: {"bid":"CP","bkey":"mcRS5***********","statId":"CP1003","chargerId":"01","btid":"188351","tbid":"ME","cardNo":"2055222001314533","pow":"64200","bprice":"324.4","tbprice":"324.4","bmon":"20567","mon":"20567","tsdt":"20240731200811","tedt":"20240801131126","rcvdate":"20240801131126"}
```

## 환경부 충전내역 등록 (응답)

| Message | Depth | Variable | DataType | 설명 |
|---|---|---|---|---|
| **충전내역 등록 (응답)** | 1 | resultCode | string | 결과코드 (000: 성공, 026/100: 실패) |
|  | 1 | resultMessage | string | 결과코드에 맞는 메시지 |
|  | 1 | resultData | string | 결과값 (환경부 서버 responseData) |

**▶ 예제 (응답)**

```json
{
  "resultCode": "000",
  "resultMessage": "resultCode에 맞는 메시지",
  "resultData": "결과값"
}
```

## 환경부 충전내역 삭제 (요청)

| Message | Depth | Variable | DataType | 설명 |
|---|---|---|---|---|
| **충전내역 삭제 (요청)** | 1 | bid | string | 기관ID  예) CP |
|  | 1 | bkey | string | 기관인증키 |
|  | 1 | statId | string | 충전소ID |
|  | 1 | chargerId | string | 충전기ID |
|  | 1 | tsdt | string | 충전 시작일시 (YYYYMMDDHHmmSS) |
|  | 1 | tedt | string | 충전 종료일시 (YYYYMMDDHHmmSS) |

**▶ 예제 (POST)**

```
POST https://castprocsms.kr:3003/charge/unregisterChargeHistory body: {"bid":"CP","bkey":"mcRS5***********","statId":"CP1003","chargerId":"01","tsdt":"20240731200811","tedt":"20240801131126"}
```

## 환경부 충전내역 삭제 (응답)

| Message | Depth | Variable | DataType | 설명 |
|---|---|---|---|---|
| **충전내역 삭제 (응답)** | 1 | resultCode | string | 결과코드 (000: 성공, 026/100: 실패) |
|  | 1 | resultMessage | string | 결과코드에 맞는 메시지 / 실패 원인 |
|  | 1 | resultData | string | 결과값 또는 "환경부 미연동 회원사" 메시지 |

**▶ 예제 (응답)**

```json
{
  "resultCode": "000",
  "resultMessage": "resultCode에 맞는 메시지",
  "resultData": "결과값 또는 {message: 환경부 미연동 회원사}"
}
```
