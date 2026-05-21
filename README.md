# AWS Summit Seoul 후기 HTML PPT MVP

AWS Summit Seoul 2026을 다녀온 후기를 HTML 발표 자료처럼 만든 정적 웹 프로젝트입니다.
보라/마젠타 조명, 검정 배경, 큰 흰색 타이포, 현장 사진 무드를 기준으로 구성했습니다.

## 파일 구조

```text
.
├── index.html
└── assets/
    └── images/
        ├── summit-build-together.jpg
        ├── summit-entrance.jpg
        ├── summit-expo-map.jpg
        ├── summit-keynote-side.jpg
        ├── summit-stage-icons.jpg
        ├── summit-stage-portrait.jpg
        └── summit-wide-stage.jpg
```

## 로컬 실행

가장 간단한 방법은 `index.html`을 브라우저로 직접 여는 것입니다.

```powershell
Start-Process .\index.html
```

개발 서버로 보고 싶고 Python이 설치되어 있으면 프로젝트 폴더에서 아래 명령을 실행합니다.

```powershell
python -m http.server 5173
```

그 다음 브라우저에서 아래 주소를 엽니다.

```text
http://localhost:5173
```

Python이 설치되어 있지 않다면 VS Code의 Live Server 확장처럼 정적 파일을 띄울 수 있는 도구를 사용해도 됩니다.

발표 조작:

- 오른쪽 방향키, Space, PageDown: 다음 슬라이드
- 왼쪽 방향키, PageUp: 이전 슬라이드
- Home: 첫 슬라이드
- End: 마지막 슬라이드
- F: 전체 화면 전환

## AWS Amplify Hosting 배포

MVP는 백엔드가 없는 정적 사이트이므로 `AWS Amplify Hosting`으로 배포하는 것이 가장 쉽습니다.

1. 이 폴더를 GitHub 저장소에 업로드합니다.
2. AWS 콘솔에서 `AWS Amplify`로 이동합니다.
3. `Deploy an app` 또는 `Host web app`을 선택합니다.
4. GitHub 저장소와 브랜치를 연결합니다.
5. 빌드 설정은 정적 HTML이므로 특별한 빌드 명령 없이 배포합니다.
6. 배포가 끝나면 Amplify 기본 주소가 생성됩니다.

예상 기본 주소 형태:

```text
https://main.xxxxxxxx.amplifyapp.com
```

## AWS에서 도메인 구입하기

AWS에서는 `Amazon Route 53`에서 도메인을 검색하고 구매할 수 있습니다.

주의할 점:

- 도메인은 보통 1년 단위로 구매합니다.
- `.com`, `.net`, `.org` 등 TLD마다 가격이 다릅니다.
- AWS 프로모션 크레딧은 Route 53 도메인 등록 비용에 적용되지 않을 수 있습니다.
- Route 53 Hosted Zone은 월 과금이 있습니다. 공식 가격 기준 첫 25개 Hosted Zone은 월 `$0.50`입니다.

도메인 구매 흐름:

1. AWS 콘솔에서 `Route 53`으로 이동합니다.
2. `Registered domains` 메뉴에서 원하는 도메인을 검색합니다.
3. 사용 가능한 도메인을 장바구니에 담고 등록자 정보를 입력합니다.
4. 이메일 인증을 완료합니다.
5. 도메인 등록이 완료되면 Hosted Zone이 만들어집니다.

## Amplify에 도메인 연결하기

1. AWS Amplify 콘솔에서 배포한 앱을 엽니다.
2. `Hosting` 메뉴에서 `Custom domains`를 선택합니다.
3. Route 53에서 구매한 도메인을 선택합니다.
4. 연결할 브랜치와 서브도메인을 지정합니다.
5. Amplify가 DNS 레코드와 HTTPS 인증서 구성을 진행합니다.

최종 주소 예시:

```text
https://aws-summit-review.com
https://www.aws-summit-review.com
```

## 현재 슬라이드 구성

총 14장입니다.

1. 표지
2. AWS Summit Seoul 행사 개요
3. 연설 핵심 지도
4. 핵심 1: AI-DLC 개념
5. AI-DLC 기존 방식과 차이점
6. 핵심 2: AWS Kiro
7. 핵심 3: Amazon Quick
8. 3M의 Amazon Quick Suite 활용 사례
9. Agentic AI
10. Physical AI
11. Expo Hall에서 보인 흐름
12. 내가 찍은 사진으로 남은 장면
13. 이 PPT에 AWS를 어떻게 쓸지
14. 마무리

## 참고 자료

- AWS Summit Seoul 2026 공식 페이지
- AWS Kiro 공식 문서 및 FAQ
- Kiro 공식 웹사이트 이미지: Specs/Tasks, Agent Hooks 화면
- Amazon Quick / Amazon Quick Suite 공식 페이지
- Amazon Quick 고객 사례 페이지: 3M
- Amazon Q Developer 고객 사례 페이지
- 조선비즈: AWS Summit Seoul 2026 키노트 보도
- 파이낸셜뉴스/뉴스1: AI-DLC, Agentic AI, Physical AI 관련 보도
- 동아일보: AWS Summit Seoul 2026 스타트업 존/Expo 보도

## 이 PPT에 들어간 AWS 기술 포인트

현재 MVP에서 실제로 사용할 AWS 기술:

- `AWS Amplify Hosting`: HTML 발표 사이트 배포
- `Amazon Route 53`: 도메인 구매와 DNS 관리
- `AWS Certificate Manager`: HTTPS 인증서
- `Amazon CloudFront`: Amplify 뒤에서 정적 파일을 빠르게 전달하는 CDN

나중에 추가할 수 있는 확장:

- `Amazon S3`: 발표 이미지나 자료 파일 저장
- `AWS Lambda + Amazon API Gateway`: 방명록, 피드백 폼 API
- `Amazon DynamoDB`: 피드백 데이터 저장

MVP에서는 발표 자체에 집중하고, 백엔드는 실제 기능이 필요해지는 순간에 붙이는 방식이 가장 안전합니다.

## 다음에 채워야 할 내용

슬라이드 7, 8에는 부스 상세 내용이 비어 있습니다.

아래 형식으로 내용을 정리하면 바로 반영할 수 있습니다.

```text
1. 부스/체험 이름:
2. 거기서 본 것:
3. 신기했던 점:
4. 발표에서 말하고 싶은 한 문장:
5. 관련 사진 파일:
```
