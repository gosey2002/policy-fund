# 정책자금 한도 진단 랜딩페이지

기업 정책자금 상담을 위한 단일 페이지 랜딩페이지입니다. 빌드 도구 없이 `index.html` 한 파일로 동작하며, GitHub Pages에 그대로 올려 사용할 수 있습니다.

- 운영 주소: https://fund.4usquare.co.kr/ (`CNAME` 파일 유지 필요)
- 저장소 주소: https://gosey2002.github.io/policy-fund/
- 구성: 헤더 · 히어로 · 주의사항(심사결과통보서) · 전문가 솔루션 · 생애주기별 전략 · 실적 · 4단계 절차 · 11단계 자금 진단 신청 폼 · 푸터
- 외부 라이브러리 없음(폰트만 Google Fonts · Pretendard CDN 사용)

## 디자인 시스템

메인 홈페이지 `4usquare.co.kr`(`gosey2002/4usquare`)와 동일한 토큰을 사용합니다. 색·타이포·버튼·카드·헤더·푸터를 바꿀 때는 두 저장소를 함께 맞춰 주세요.

| 토큰 | 값 |
| --- | --- |
| 폰트 | `Pretendard Variable` → `Pretendard` → `Noto Sans KR` |
| 메인 네이비 | `--navy: #0B2545` (밝은 면 `--navy-700: #123057`, 진한 면 `--navy-900: #071A33`) |
| 포인트 스틸 | `--steel: #3B6E9C` |
| 포인트 세이지 | `--sage: #8FA395` |
| 배경 · 보더 · 본문 | `--slate-50: #F8FAFC` · `--line: #E3E9F0` · `--muted: #5A6B80` |
| 모서리 | 카드 `20px`, 작은 카드 `12px`, 버튼 `999px` |

- 로고·파비콘: `assets/` (4usquare 저장소와 같은 파일)
- 헤더 로고와 `포유스퀘어 홈페이지` 버튼, 푸터 링크는 모두 https://4usquare.co.kr 로 연결됩니다.

## 신청 알림 설정 (중요)

신청 폼은 [FormSubmit](https://formsubmit.co)을 통해 메일로 접수됩니다.

1. 현재 알림 수신 주소: `realoio@naver.com` (`index.html` 안의 `var SUBMIT_EMAIL = 'realoio@naver.com';`)
2. **최초 1회**, 실제 신청을 한 번 접수하면 `realoio@naver.com`으로 FormSubmit 활성화 메일이 도착합니다. 그 메일의 **Activate Form** 링크를 눌러야 이후 접수분부터 알림 메일이 정상 전달됩니다.
3. 수신 주소를 바꾸려면 `index.html`의 `SUBMIT_EMAIL` 한 줄만 수정하고, 새 주소에서 같은 방식으로 한 번 활성화하면 됩니다.
4. 전송이 막히면(AJAX 실패) 일반 폼 POST로 자동 전환되며, 돌아온 주소의 `?submitted=1`을 보고 완료 화면을 표시합니다.

## Meta 픽셀

2027 Meta 전환 캠페인용 픽셀이 설치되어 있습니다. (`<head>`의 Meta Pixel Code)

- 픽셀 ID: `2558945831208196`
- 기본 이벤트: `PageView` (페이지 로드 시 1회)
- 전환 이벤트: `CompleteRegistration`
  - 신청 버튼을 눌러 접수를 시작할 때 1회 전송합니다. (일반 폼 POST로 넘어가기 전에도 전송)
  - `?submitted=1`로 돌아온 경우, 같은 세션에서 아직 보내지 않았을 때만 전송합니다.
  - 중복 전송 방지: `sessionStorage`의 `pf_meta_cr_fired` 값으로 1회만 전송합니다.

## 수정이 필요한 곳

| 항목 | 위치 |
| --- | --- |
| 신청 알림 이메일 | `index.html` → `var SUBMIT_EMAIL = ...` |
| 푸터 사업자 정보(상호·대표·연락처·이메일·주소) | `index.html` → `<footer class="site-footer">` |
| 개인정보처리방침 내용 | `index.html` → `<div class="policy-modal" id="privacyModal">` |
| 헤더 메뉴 | `index.html` → `<nav class="nav" id="primaryNav">` |
| Meta 픽셀 ID | `index.html` → `fbq('init', '1517998500234538')` (2곳: 스크립트·noscript) |
| 마감 문구(2026년 12월 29일 고정) | `index.html` → `var deadlineText = '12월 29일';` 와 `.pf-deadline` 기본 문구 |

## 개인정보 · 예시 표기

- 신청 폼의 개인정보 동의 영역에 `동의를 거부할 권리가 있으나, 거부 시 상담 신청이 제한됩니다.` 문구와 `[개인정보처리방침]` 링크가 있습니다.
- `[개인정보처리방침]`(동의 영역·푸터)을 누르면 수집항목·이용목적·보유기간(상담 신청일로부터 2년)·거부권·제3자 제공/처리 위탁·문의처를 담은 모달이 열립니다. ESC·배경 클릭·닫기 버튼으로 닫힙니다.
- 2026-11-28 정비: 보유기간을 `상담 종료 후 6개월` → `상담 신청일로부터 2년`으로 실제 운영(리드 보관·상담 이력 관리)에 맞추고, 위탁 표에 FormSubmit(이메일 전송 대행)·강한컴퍼니(온라인 광고 운영·상담 DB 발송·관리 대행)를 공개했으며, Meta 픽셀로 접속·이용 기록이 Meta Platforms에 전송된다는 사실을 제3자 제공 항목에 명시했습니다. 위탁 업무가 바뀌면 이 모달과 폼 동의 문구를 함께 수정해야 합니다.
- 화면의 한도·금리·실적·사례 수치는 이해를 돕기 위한 대표 예시이며, 실제 조건은 기업의 신용도·재무 현황에 따라 달라질 수 있다는 안내를 히어로·심사결과통보서 아래·실적 하단·푸터에 표기했습니다.
- 사업자등록번호는 푸터에 표기하지 않습니다.

## 로컬 확인

`index.html`을 브라우저로 열면 그대로 동작합니다. (폰트를 불러오려면 인터넷 연결 필요)
