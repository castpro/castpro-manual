# 카드 인증(회원구분 조회) REST API

> 원본: `ocpp_api_rest_api_spec260707.docx` (OCPP 메시지 & REST API 명세)

> **※ 참고**
>
> Base URL: https://castprocsms.kr:3003
>
> 호출 방식: REST GET
>
> RFID 카드 태깅 시 OCPP Authorize 호출 이전에, 카드번호로 발급 기관(bid)을 조회하는 선행 호출입니다.
>
> ME는 환경부, CC는 신용카드로 사용 중입니다.
>
> CP처럼 회원/로밍회원의 경우, bid는 해당 카드가 속한 회원사의 bid와 동일하게 나옵니다.
>
> 인증이 된 카드에 한해서, 회원사 bid와 같으면 회원, 다르면 로밍회원으로 구분합니다.

## 회원구분 조회 (요청)

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| 회원구분 조회 (요청) | 1 | cardNo | string | 조회할 카드(RFID/IC카드) 번호 | REST GET |

**▶ 예제**

```
GET https://castprocsms.kr:3003/user/authorizeWithCardno?cardNo=1098112100000049
```

## 회원구분 조회 (응답)

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| 회원구분 조회 (응답) | 1 | resultCode | string | 결과코드 (000: 성공, 그 외 에러) |  |
|  |  | resultMessage | string | 결과메시지 |  |
|  |  | resultData | array | 카드 발급 기관(bid) 조회 결과 배열 |  |
|  | 2 | bid | string | 카드 발급 기관 bid (ME: 환경부 카드, CC: 신용카드, CP: 회원사 bid 예시) |  |

**▶ 예제**

```json
{
  "resultCode": "000",
  "resultMessage": "successful",
  "resultData": [
    {
      "bid": "ME"
    }
  ]
}
```

## 문의처

| 담당자 | 캐스트프로 연구소 |
|---|---|
| **전화** | 070-4855-2090 |
| **이메일** | rnd@castpro.kr |
