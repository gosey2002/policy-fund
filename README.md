# 정책자금 한도 진단 랜딩페이지

기업 정책자금 상담을 위한 단일 페이지 랜딩페이지입니다. 빌드 도구 없이 `index.html` 한 파일로 동작하며, GitHub Pages에 그대로 올려 사용할 수 있습니다.

- 페이지 주소: https://gosey2002.github.io/policy-fund/
- 구성: 히어로 · 주의사항(심사결과통보서) · 전문가 솔루션 · 생애주기별 전략 · 실적 · 4단계 절차 · 11단계 자금 진단 신청 폼 · 푸터
- 외부 라이브러리 없음(폰트만 Google Fonts · Pretendard CDN 사용)

## 신청 알림 설정 (중요)

신청 폼은 [FormSubmit](https://formsubmit.co)을 통해 메일로 접수됩니다.

1. 현재 알림 수신 주소: `realoio@naver.com` (`index.html` 안의 `var SUBMIT_EMAIL = 'realoio@naver.com';`)
2. **최초 1회**, 실제 신청을 한 번 접수하면 `realoio@naver.com`으로 FormSubmit 활성화 메일이 도착합니다. 그 메일의 **Activate Form** 링크를 눌러야 이후 접수분부터 알림 메일이 정상 전달됩니다.
3. 수신 주소를 바꾸려면 `index.html`의 `SUBMIT_EMAIL` 한 줄만 수정하고, 새 주소에서 같은 방식으로 한 번 활성화하면 됩니다.

## 수정이 필요한 곳

| 항목 | 위치 |
| --- | --- |
| 신청 알림 이메일 | `index.html` → `var SUBMIT_EMAIL = ...` |
| 푸터 사업자 정보(대표·이메일·연락처·주소) | `index.html` → `<footer class="pf-footer">` |
| 상호·사업자등록번호 | 푸터 주석 처리된 부분을 풀어서 입력 |
| 마감 문구(매월 말일 자동 표시) | 스크립트가 자동 계산하므로 수정 불필요 |

## 로컬 확인

`index.html`을 브라우저로 열면 그대로 동작합니다. (폰트를 불러오려면 인터넷 연결 필요)
