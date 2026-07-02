# install-cert-reject-reason

설치인증 검토 모달에 **반려 사유 드롭다운(필수)** 을 추가한 동작 프로토타입.

## 🔗 라이브 데모

https://delicate2330.github.io/install-cert-reject-reason/

> 데모 데이터는 전부 더미값(김철수 등)입니다. 실제 고객 정보 아님.

## 개요

"설치인증 반려" 버튼을 누르기 전에 반드시 반려 사유를 선택하도록 강제한다. 사유를 고르지 않으면 반려 버튼이 비활성화되고, 반려 시 선택값이 서버로 전송된다.

## 동작

- 사유 미선택 → 반려 버튼 비활성(회색)
- 사유 선택 → 반려 버튼 활성화
- "기타 (직접입력)" 선택 → 텍스트 입력창 노출, 입력해야 반려 가능
- 반려 클릭 → `POST`로 payload 전송 (엔드포인트 미연동 시 전송될 payload를 토스트로 표시)

## 반려 사유 목록

| 라벨 | 코드값 |
|---|---|
| 캡처 화면(스크린샷) 제출 | `screenshot` |
| 무관한 사진(오첨부) | `irrelevant_photo` |
| 제품 식별 불가 (원거리/저화질) | `product_unidentifiable` |
| 설치 미완료 | `install_incomplete` |
| 제품 불이치 | `product_mismatch` |
| 제품 미개봉(미설치) | `unopened` |
| 기타 (직접입력) | `etc` |

## 서버 연동

`index.html` 하단 스크립트의 두 값만 실제 값으로 교체하면 된다.

```js
var API_ENDPOINT = '/api/admin/install-cert/reject'; // 실제 반려 API 엔드포인트
var USID = '0000000'; // 견적 USID (실제로는 서버/props에서 주입)
```

전송 payload:

```json
{
  "usid": "0000000",
  "reasonCode": "screenshot",
  "reasonLabel": "캡처 화면(스크린샷) 제출",
  "reasonText": "캡처 화면(스크린샷) 제출",
  "rejectedAt": "2026-07-02T00:00:00.000Z"
}
```

## 주의

Public 레포 + GitHub Pages라 데모 URL은 누구나 접근 가능하다. 데모 종료 후 Pages 비활성화 또는 레포 삭제를 권장.
