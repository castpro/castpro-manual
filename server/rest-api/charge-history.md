# 충전이력 등록 REST API

> 원본: `ocpp_api_rest_api_spec260707.docx` (OCPP 메시지 & REST API 명세)

> **※ 참고**
>
> Endpoint: POST https://castprocsms.kr:3003/charge/registerChargeHistory
>
> 호출 방식: REST POST (body: JSON)
>
> btid: StartTransaction.conf으로부터 할당받은 transactionId를 내부 거래 식별번호로 사용

## 충전이력등록 (요청)

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **충전이력등록 (요청)** | 1 | bid | string | 기관ID | REST POST |
|  |  | bkey | string | 기관인증키 |  |
|  |  | cardNo | string | 회원카드번호 (신용카드 결제 시 기본값 할당) |  |
|  |  | statId | string | 충전소ID |  |
|  |  | chargerId | string | 충전기ID |  |
|  |  | tbid | string | 회원카드 소속기관ID |  |
|  |  | tsdt | string | 충전 시작일시 (YYYYMMDDHHmmSS) |  |
|  |  | tedt | string | 충전 종료일시 (YYYYMMDDHHmmSS) |  |
|  |  | btid | string | 기관거래ID (StartTransaction.conf의 transactionId) |  |
|  |  | pow | string | 충전량 [Wh] |  |
|  |  | mon | string | 충전금액 |  |
|  |  | bprice | string | 충전기관 단가 |  |
|  |  | tbprice | string | 회원카드 소속기관 단가 |  |
|  |  | bmon | string | 충전기관 금액 |  |
|  |  | rcvdate | string | 수신일시 |  |

**▶ 예제**

```
POST https://castprocsms.kr:3003/charge/registerChargeHistory body: {"bid":"CP","bkey":"mcRS5***********","bmon":"70","bprice":"176.0","btid":"53561","cardNo":"9002021702170217","chargerId":"01","mon":"70","pow":"400","rcvdate":"20230210084530","statId":"D00001","tsdt":"20230210084110","tedt":"20230210084530"}
```

## 충전이력등록 (응답)

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **충전이력등록 (응답)** | 1 | resultCode | string | 결과코드 (000: 성공, 그 외 에러) |  |
|  |  | resultMessage | string | 결과메시지 (successful / 에러내용) |  |
|  |  | resultData | array | 환경부 서버로부터 수신한 responseData |  |

**▶ 예제**

```json
{     "resultCode": "000",     "resultMessage": "successful",     "resultData": "{"affectedRows":"1"}" }
```
