# STAY DIMANSION Design System

Editorial Stay — 머무는 시간을 편집하는 스테이 / *Stay with comfort, connect with ease.*

이 저장소는 인천 미추홀구 게스트하우스 **STAY DIMANSION(스테이디멘션)** 의 디자인 시스템입니다. 읽기 전용 참조용입니다.

## ChatGPT에게 (먼저 읽을 것)

새 디자인, 이미지, 문구를 만들기 전에 이 README 전체와 `design-system.md`, `tokens.css`를 읽고, 아래 규칙을 지켜 작업하세요. 시각 예시는 `swatches.png`와 `examples/`에 있습니다. 규칙과 사용자 요청이 충돌하면 사용자에게 먼저 물어보세요.

답변은 한국어로 하고, 영어 병기가 필요한 곳은 함께 씁니다. 시안을 낼 때는 사용한 색(HEX), 글꼴, 여백 의도를 한 줄씩 먼저 밝힌 뒤 결과를 보여주세요.

## 1. 브랜드

- 이름: **STAY DIMANSION** (대문자, 두 단어). 한글 표기는 스테이디멘션.
- 태그라인: 머무는 시간을 편집하는 스테이 / Stay with comfort, connect with ease.
- 분위기: 조용함, 흙과 리넨의 색, 넓은 여백, 얇은 선. 정중하지만 차갑지 않게.

## 2. 색

| 이름 | HEX | CMYK | 용도 |
|---|---|---|---|
| Page | `#F6F2E6` | C3 M4 Y10 K0 | 바탕, 전체의 약 80% |
| Page Deep | `#EFE6D6` | C6 M7 Y15 K0 | 한 단계 진한 바탕 |
| Linen | `#E2D6BD` | C10 M11 Y24 K1 | 구분 면, 선 |
| Ink | `#1F1A16` | 글자는 K100 | 글자와 구조, 약 15% |
| Ink 70 | `#5B5249` | C34 M36 Y42 K56 | 보조 글자 |
| Olive | `#6E695B` | C35 M32 Y43 K43 (작은 글자는 K62) | 라벨, 캡션 |
| Ink 40 | `#A39A87` | C28 M24 Y36 K13 (선은 K38) | 가는 선 |
| Rust | `#8C3A2D` | C36 M89 Y83 K13 | 강조. 한 장에 한두 곳. 본문 글자색 금지 |
| Rust Deep | `#5D231C` | C47 M84 Y67 K47 | 강조의 눌림 상태 |
| Brass | `#B69A5B` | C24 M31 Y74 K2 | 장식 전용. 글자 금지(대비 2.1:1) |

- 비율: 바탕 약 80 : 잉크 약 15 : 러스트+브라스 약 5.
- 인쇄물은 러스트를 면 바탕으로 쓸 수 있음(명함 뒷면, 스티커). 화면에서는 강조 한두 곳만.
- 금지: 채도 높은 색, 그라데이션, 그림자, 네온.

## 3. 글꼴

- **Hahmlet**: 제목, 로고 글자, 리드 문장, 인용. (Google Fonts)
- **Pretendard**: 본문과 UI. 불러올 수 없으면 Noto Sans KR.
- **이탤릭 금지.** 제3의 글꼴, 장식 글꼴 금지.
- 한글과 영문이 한 줄에 있으면 영문·숫자를 약 10% 크게 (예: 한글 9.5, 영문 10.5).
- 작은 라벨은 대문자, 자간 0.08~0.12em.
- **한국어 줄바꿈은 단어 단위**: CSS `word-break: keep-all; overflow-wrap: break-word;`. 단어나 음절이 중간에서 끊기지 않게 줄을 나눕니다. 일본어·중국어는 `word-break: normal; line-break: strict;`로 두고, 가타카나 단어와 버튼 이름은 `white-space: nowrap`으로 묶습니다.

## 4. 형태와 레이아웃

- 각진 면, 1px 헤어라인, 평평한 색 면. 모서리 반경 0~2px (스티커 재단선만 2.5mm).
- 그림자, 입체 효과, 장식 아이콘, 이모지 금지.
- **여백이 먼저.** 본문을 채우지 않고 요소를 하나씩 세웁니다. 정보를 쪼개고 넉넉히 비웁니다.
- 12열 그리드, 간격은 4의 배수.
- 사진: 따뜻한 크림·호박빛 톤. 꽉 채우거나 넓은 여백과 함께 씁니다.

## 5. 로고

- 원(방사선으로 나뉜 원) + STAY DIMANSION 글자. `logos/`의 파일만 사용하고, 다시 그리거나 비율을 바꾸지 않습니다.
- 밝은 바탕은 잉크색, 러스트·잉크 바탕은 아이보리색.
- 선이 가늘어서 작은 크기의 4도 역상 인쇄는 피합니다.
- 파일: `logos/logo-stay-horizontal-ink.png`, `logo-stay-horizontal-ivory.png`, `logo-stay-stacked-ink.png`, `logo-stay-stacked-ivory.png`, `logo-symbol.jpg`(글자 없는 원).

## 6. 말투

- 짧은 문장, 마침표로 끝냅니다.
- 느낌표, 이모지, 과장 형용사("강력추천", "완벽") 금지.
- 할인과 기한으로 압박하지 않습니다.
- 이유부터 말하고, 구체적으로 씁니다(소재, 시간).
- 예: "오후 세 시에 문을 엽니다. 커피는 로비에 있고, 옥상은 밤 열한 시까지 열려 있습니다."
- 인쇄물은 한국어와 English를 함께, 영문은 짧게. 필요하면 日本語, 中文.
- 알레르기는 표준 표기 "알레르기"를 씁니다.

## 7. 인쇄

- CMYK, 재단선에서 3mm 도련(스티커는 2mm), 글자와 로고는 재단선 안쪽 3mm 이상.
- 작은 글자와 가는 선은 K 단색. 러스트 별색 후보: PANTONE 7594 C.
- 크기 예: 명함 90×50mm, 엽서 100×148mm, 스티커 65×88mm, POP은 A5/A4.

## 8. 이미지를 만들 때

이미지 프롬프트에는 위 규칙을 영어로 풀어 쓰세요. 예:
*warm cream paper background (#F6F2E6), ink-black thin hairline details, one muted rust-red accent (#8C3A2D), generous empty space, quiet editorial mood, no gradients, no shadows, no italic type, no emoji.*
이미지 속 글자는 글꼴이 정확히 나오지 않으므로 최소로 하거나, 글자를 얹을 자리를 비워 두세요.

## 9. 기본 정보

- 주소: 인천광역시 미추홀구 인주대로131번길 6 스테이디멘션
- 홈페이지: https://dimansion.kr/ · 인스타그램: @dimansion_official
- 문의: 010-9730-4120 · staydimansion@gmail.com

## 파일

| 파일 | 내용 |
|---|---|
| `README.md` | 이 문서 (핵심 규칙) |
| `design-system.md` | 디자인 시스템 상세 설명 (영문, 결정 기록 포함) |
| `tokens.css` | 색, 글꼴, 간격, 인쇄 값, 줄바꿈 규칙 (CSS 변수) |
| `swatches.png` | 색, 글꼴, 규칙, 로고를 한 장에 모은 견본 |
| `logos/` | 로고 파일 |
| `examples/` | 적용 예시: 엽서 앞면 2종, 엽서 뒷면, 빵봉지 스티커 |

## 관련 저장소

직원용 앱 화면(`dimension-crew`)과 하우스룰·웰컴카드 캔버스는 별도 저장소 [dimansion-design](https://github.com/staydimansion-hue/dimansion-design)의 규칙(예: Cormorant Garamond, Maru Buri)을 따릅니다. 이 저장소는 명함, 엽서, 안내문, POP, 스티커 같은 인쇄·홍보물의 기준입니다. 어느 쪽 소재인지 불분명하거나 두 규칙이 충돌하면 사용자에게 먼저 물어보세요.

© STAY DIMANSION. 참조용으로 공개합니다. 로고와 사진 등 자산의 재사용·재배포 권리는 소유자에게 있습니다.
