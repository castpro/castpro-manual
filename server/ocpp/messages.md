# OCPP 1.6 WebSocket 메시지

> 원본: `ocpp_api_rest_api_spec260707.docx` (OCPP 메시지 & REST API 명세)

> **※ 참고**
>
> WebSocket 주소: castproocpp.kr:3000/ocpp/{충전소ID(statId)}  예) castproocpp.kr:3000/ocpp/100116
>
> 메시지 포맷: [MessageTypeId, UniqueId, Action, Payload]  (요청) / [MessageTypeId, UniqueId, Payload]  (응답)
>
> MessageTypeId — 2: Call (요청), 3: CallResult (응답), 4: CallError (에러)

## Authorize.req

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **Authorize.req** | 1 | idTag | IdToken | 신용카드: 9001021702170217 (고정값 사용) | WEBSOCKET |

**▶ 예제**

```json
[
  2,
  "61476204510672",
  "Authorize",
  {
    "idTag": "9001021702170217"
  }
]
```

## Authorize.conf

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **Authorize.conf** | 1 | idTagInfo | IdTagInfo |  |  |
|  | 2 | expiryDate |  |  |  |
|  | 2 | parentIdTag | CiString255Type |  |  |
|  | 2 | status | AuthorizationStatus | Accepted / Blocked / Expired / Invalid / ConcurrentTx |  |

**▶ 예제**

```json
[
  3,
  "61476204510672",
  {
    "idTagInfo": {
      "status": "Accepted",
      "expiryDate": "2034-08-19T08:35:03Z",
      "parentIdTag": "NOT_USED"
    }
  }
]
```

## BootNotification.req

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **BootNotification.req** | 1 | chargeBoxSerialNumber | CiString25Type |  |  |
|  | 1 | chargePointModel | CiString20Type |  |  |
|  | 1 | chargePointSerialNumber | CiString25Type |  |  |
|  | 1 | chargePointVendor | CiString20Type |  |  |
|  | 1 | firmwareVersion | CiString50Type |  |  |
|  | 1 | iccid | CiString20Type |  |  |
|  | 1 | imsi | CiString20Type |  |  |
|  | 1 | meterSerialNumber | CiString25Type |  |  |
|  | 1 | meterType | CiString25Type |  |  |

**▶ 예제**

```json
[
  2,
  "61476204254391",
  "BootNotification",
  {
    "chargeBoxSerialNumber": "CBSERNO",
    "chargePointModel": "CSC-7000A7",
    "chargePointSerialNumber": "10011601",
    "chargePointVendor": "캐스트프로",
    "firmwareVersion": "2.0.47"
  }
]
```

## BootNotification.conf

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **BootNotification.conf** | 1 | currentTime | dateTime |  |  |
|  | 1 | interval | integer |  |  |
|  | 1 | status | RegistrationStatus | Accepted / Pending / Rejected |  |
|  | 1 | bid | string | 환경부 기관ID |  |
|  | 1 | bkey | string | 환경부 기관 인증키 |  |
|  | 1 | member\_id | string | 회원사 ID (기본: castpro) |  |

**▶ 예제**

```json
[
  3,
  "61476204254391",
  {
    "status": "Accepted",
    "currentTime": "2024-08-19T08:30:46Z",
    "interval": 90,
    "statId": "100116",
    "member_id": "castpro",
    "bid": "CP",
    "bkey": "mcRS5***********"
  }
]
```

## StartTransaction.req

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **StartTransaction.req** | 1 | idTag | IdToken | 신용카드: 9001021702170217 (고정값 사용) | WEBSOCKET |
|  | 1 | meterStart | integer |  |  |
|  | 1 | timestamp | dateTime |  |  |
|  | 1 | bid | string | 환경부 기관ID |  |
|  | 1 | bkey | string | 환경부 기관 인증키 |  |
|  | 1 | connectorId | integer | 충전소ID+충전기ID  예) 충전소ID:100116, 충전기ID:01 → 10011601 |  |

**▶ 예제**

```json
[
  2,
  "61476204520796",
  "StartTransaction",
  {
    "bid": "CP",
    "bkey": "mcRS5***********",
    "connectorId": "10011601",
    "idTag": "9001021702170217",
    "meterStart": 110600,
    "reservationId": 0,
    "timestamp": "2024-08-19T17:35:12Z"
  }
]
```

## StartTransaction.conf

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **StartTransaction.conf** | 1 | idTagInfo | IdTagInfo |  |  |
|  | 1 | transactionId | integer |  |  |

**▶ 예제**

```json
[
  3,
  "61476204520796",
  {
    "transactionId": 194713,
    "idTagInfo": {
      "status": "Accepted",
      "expiryDate": "2034-08-19T08:35:13Z",
      "parentIdTag": "NOT_USED"
    }
  }
]
```

## StopTransaction.req

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **StopTransaction.req** | 1 | idTag | IdToken | 신용카드: 9001021702170217 (고정값 사용) | WEBSOCKET |
|  | 1 | meterStop | integer |  |  |
|  | 1 | timestamp | dateTime |  |  |
|  | 1 | transactionId | integer |  |  |
|  | 1 | reason | Reason |  |  |
|  | 1 | bid | string | 환경부 기관ID |  |
|  | 1 | bkey | string | 환경부 기관 인증키 |  |
|  | 1 | connectorId | integer | 충전소ID+충전기ID  예) 충전소ID:100116, 충전기ID:01 → 10011601 |  |

**▶ 예제**

```json
[
  2,
  "30982896811196",
  "StopTransaction",
  {
    "bid": "CP",
    "bkey": "mcRS5***********",
    "connectorId": "10011601",
    "idTag": "9001021702170217",
    "meterStop": 800,
    "reason": "Local",
    "timestamp": "2023-04-03T14:49:22Z",
    "transactionId": 68703
  }
]
```

## StopTransaction.conf

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **StopTransaction.conf** | 1 | idTagInfo | IdTagInfo |  |  |

**▶ 예제**

```json
[
  3,
  "30982896811196",
  {
    "idTagInfo": {
      "status": "Accepted",
      "parentIdTag": "NOT_USED",
      "expiryDate": "2033-04-03T05:49:23Z"
    }
  }
]
```

## MeterValues.req

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **MeterValues.req** | 1 | connectorId | integer | 충전소ID+충전기ID  예) 충전소ID:100116, 충전기ID:01 → 10011601 |  |
|  | 1 | transactionId | integer |  |  |
|  | 1 | meterValue | MeterValue Object array |  |  |
|  | 2 | timestamp | dateTime |  |  |
|  | 2 | sampledValue | SampledValue Array |  |  |
|  | 3 | value | String |  |  |
|  | 3 | context | ReadingContext Enum |  |  |
|  | 3 | format | ValueFormat Enum |  |  |
|  | 3 | measurand | Measurand Enum |  |  |

**▶ 예제**

```json
{
  "connectorId": 1,
  "meterValue": [
    {
      "sampledValue": [
        {
          "context": "Sample.Periodic",
          "format": "Raw",
          "location": "Outlet",
          "measurand": "Energy.Active.Import.Register",
          "unit": "kWh",
          "value": "4.2"
        }
      ],
      "timestamp": "2022-03-11T11:39:49Z"
    }
  ],
  "transactionId": 41
}
```

## MeterValues.conf

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **MeterValues.conf** |  | - | - | - |  |

## StatusNotification.req

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **StatusNotification.req** | 1 | connectorId | integer | 충전소ID+충전기ID  예) 충전소ID:100116, 충전기ID:01 → 10011601 |  |
|  | 1 | timestamp | dateTime |  |  |
|  | 1 | errorCode | string |  |  |
|  | 1 | status | string |  |  |
|  | 1 | info | string |  |  |

**▶ 예제**

```json
[
  2,
  "61476204639515",
  "StatusNotification",
  {
    "connectorId": "10011601",
    "errorCode": "NoError",
    "status": "Available",
    "timestamp": "2024-08-19T17:37:11Z"
  }
]
```

## StatusNotification.conf

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **StatusNotification.conf** |  | - | - | - |  |

**▶ 예제**

```json
[
  3,
  "61476204639515",
  {}
]
```

## Heartbeat.req

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **Heartbeat.req** | 1 | connectorId | integer | 충전소ID+충전기ID  예) 충전소ID:100116, 충전기ID:01 → 10011601 |  |

**▶ 예제**

```json
[
  2,
  "61476204758968",
  "Heartbeat",
  {
    "connectorId": "10011601"
  }
]
```

## Heartbeat.conf

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **Heartbeat.conf** |  | - | - | - |  |

**▶ 예제**

```json
[
  3,
  "61476204758968",
  {
    "currentTime": "2024-08-19T08:39:11Z"
  }
]
```

## UpdateFirmware.req

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **UpdateFirmware.req** | 1 | location | anyURI |  |  |
|  | 1 | retries | integer | optional, 재시도 횟수 |  |
|  | 1 | retrieveDate | dateTime |  |  |
|  | 1 | retryInterval | integer | optional, 재시도 간격 (단위: 초) |  |

**▶ 예제**

```json
{
  "location": "ftp://13.209.84.98/fwUpdate.apk",
  "retrieveDate": "2022-04-26T09:54:35Z"
}
```

## UpdateFirmware.conf

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **UpdateFirmware.conf** |  | - | - | - |  |

## FirmwareStatusNotification.req

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **FirmwareStatusNotification.req** | 1 | status | FirmwareStatus |  |  |

**▶ 예제**

```json
{
  "status": "Downloading"
}
```

## FirmwareStatusNotification.conf

| Message | Depth | Variable | DataType | 설명 | 호출 방식 |
|---|---|---|---|---|---|
| **FirmwareStatusNotification.conf** |  | - | - | - |  |

## 필수 · 선택 파라미터 정리

| 메시지 | 필수 파라미터 | 선택 파라미터 |
|---|---|---|
| **Authorize** | idTag: 카드번호 | — |
| **BootNotification** | chargePointSerialNumber: 충전소ID+충전기ID | firmwareVersion: 펌웨어 버전 |
| **StartTransaction** | connectorId: 충전소ID+충전기ID<br>idTag: 카드번호<br>meterStart: 충전 시작 전력<br>timestamp: 이벤트 발생시간 | bid: 기관ID (기본: 회원사 bid)<br>bkey: 기관키 (기본: 회원사 bkey) |
| **StopTransaction** | connectorId: 충전소ID+충전기ID<br>idTag: 카드번호<br>meterStop: 충전 종료 전력<br>transactionId: 트랜잭션ID<br>timestamp: 이벤트 발생시간 | bid / bkey: 기관ID/키<br>reason: 종료 이유<br>pow / mon / price: 충전량·금액·단가<br>*※ 세 값 모두 포함 시 환경부 결제 시도* |
| **Heartbeat** | connectorId: 충전소ID+충전기ID | — |
| **StatusNotification** | connectorId: 충전소ID+충전기ID<br>status: 상태값<br>AVAILABLE·FINISHING→'2', CHARGING→'3'<br>UNAVAILABLE·FAULTED→'5', RESERVED→'6'<br>timestamp: 이벤트 발생시간 | errorCode: 현재 에러코드<br>bid / bkey: 기관ID/키 |
| **FirmwareStatus Notification** | connectorId: 충전소ID+충전기ID<br>status: FIRST·Installed·Installing·Downloaded·Downloading | firmwareVersion: 펌웨어 버전<br>statId: 충전소ID |

