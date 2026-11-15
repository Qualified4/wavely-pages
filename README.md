# Wavely 공식 홈페이지

공식 소개 및 한국어·영어 개인정보처리방침만 제공하는 공개 정적 사이트입니다.
Wavely 앱은 공개 배포하지 않습니다. 앱 소스, OAuth 설정, 사용자 데이터와 미디어는 이 저장소에 포함하지 않습니다.

- 홈: https://wavely.prandiel.dev
- 개인정보처리방침: https://wavely.prandiel.dev/privacy
- English privacy: https://wavely.prandiel.dev/en/privacy
- GitHub Pages: https://qualified4.github.io/wavely-pages/ (커스텀 도메인으로 이동)

## 편집과 로컬 확인

Python 3의 표준 라이브러리만 사용합니다. Node, 패키지 설치, 백엔드, DB, 런타임 JavaScript는 필요 없습니다.

```sh
python build.py
python -m http.server 8713 --bind 127.0.0.1
```

http://127.0.0.1:8713 에서 확인합니다. `build.py`가 HTML을 생성하고 `styles.css`가 공통 스타일을 제공합니다. `site.json`의 `support_email`과 `effective_date`가 공개 연락처·시행일 설정입니다. 변경 후 빌드하여 생성된 HTML도 함께 커밋합니다.

`privacy/index.html`, `en/privacy/index.html`로 실제 디렉터리를 제공하므로 직접 접속·새로고침이 가능합니다. 확장자 없는 경로는 GitHub Pages가 끝에 `/`를 붙여 정상 페이지로 이동시킵니다. 상대 경로 자산은 프로젝트 Pages 주소에서도 작동합니다.

## 배포

GitHub Pages에서 **Deploy from a branch → main → /(root)** 를 사용합니다. 별도 앱 저장소나 워크플로는 수정하지 않습니다. `CNAME`과 Custom domain은 `wavely.prandiel.dev`, HTTPS 강제 사용을 설정합니다. DNS에는 다음 레코드만 필요합니다.

| Type | Name | Target | Proxy |
|---|---|---|---|
| CNAME | wavely | qualified4.github.io | DNS only |

기존 다른 서브도메인의 DNS와 Pages는 변경하지 않습니다.

## Google Cloud 입력값

Google Cloud의 **Wavely** 프로젝트에서 **Google Auth Platform → Branding**을 엽니다.

| 항목 | 값 |
|---|---|
| 앱 이름 | Wavely |
| 사용자 지원 이메일 | davin3377@gmail.com |
| 홈페이지 | https://wavely.prandiel.dev |
| 개인정보처리방침 | https://wavely.prandiel.dev/privacy |
| 승인된 도메인 | prandiel.dev |
| OAuth 클라이언트 | Wavely Desktop / Desktop app |
| 로고 | icon.png (PNG, 256×256, 1,241 bytes) |

로고는 기존 Wavely 앱의 아이콘을 그대로 복사한 파일입니다. [공식 요구사항](https://support.google.com/cloud/answer/15549049)에 명시된 PNG·정사각형·1MB 이하 조건을 만족합니다. Google은 최적 표시 크기로 120×120을 권장합니다. 현재 로고는 256×256이며 심사 승인 여부는 Google에서 결정합니다.

1. Google Search Console에서 `prandiel.dev` 소유권을 프로젝트 소유자·편집자 계정으로 확인합니다. 기존 검증이 있다면 재사용합니다.
2. 위 값과 로고를 입력하고 개발자 연락처를 확인합니다. 지원 이메일은 Console에서 선택 가능한 프로젝트 계정 또는 적절한 Google Group 주소여야 합니다.
3. Branding에서 검증을 요청하고 결과를 확인한 뒤 브랜딩을 게시합니다. Google의 검증이 끝나기 전 승인된 것으로 표현하지 않습니다.
4. Data Access에 실제 요청하는 `https://www.googleapis.com/auth/youtube.force-ssl`을 선언합니다. 브랜딩 검증과 민감한 범위 데이터 액세스 검증은 별도 절차입니다. 필요한 경우 Verification Center에 기능 시연 영상과 권한 필요 근거를 제출합니다.
5. 개인 전용·개발/테스트 앱은 [검증 예외](https://developers.google.com/identity/protocols/oauth2/production-readiness/brand-verification#exceptions)에 해당할 수 있습니다. 실제 사용자 범위와 Console 안내를 기준으로 판단합니다. 이 사이트를 공개했다고 앱을 공개 배포하거나 심사를 통과한 것은 아닙니다.

Desktop app 클라이언트 ID·Client Secret·설정 JSON은 사이트나 저장소에 넣지 않습니다. 홈페이지 도메인을 Desktop app의 웹 리디렉션 URI로 등록할 필요도 없습니다.

## 심사 전에 별도로 확인할 앱 사항

시행일에 확인한 로컬 편집 기능과 개발 중 계정 기능을 구분해 공개했습니다. 토큰의 Windows DPAPI 보관, Google과의 직접 통신, 연결 해제 후 남는 기록과 수동 삭제 절차를 설명합니다. 실제 업로드의 전체 동작 검증은 이 홈페이지 작업 범위에 포함하지 않습니다.

[YouTube 개발자 정책](https://developers.google.com/youtube/terms/developer-policies)의 III.E에는 API 데이터 갱신·삭제 조건, 앱 내 동의 철회 후 7일 이내 삭제, Google 설정에서 철회한 경우 30일 이내 삭제 조건이 있습니다. 현재 앱에서 해당 자동 정리나 전용 기록 삭제 기능은 확인되지 않았습니다. 수동 삭제 안내가 자동으로 정책 준수를 보장하지 않으므로 앱 개발 측에서 검토해야 합니다.

같은 정책 III.E의 Audiovisual Content는 YouTube 사전 서면 승인 없는 시청각 콘텐츠 다운로드·보관 등을 제한합니다. yt-dlp를 통한 가져오기 기능도 포함하여 실제 앱의 정책 적합성과 필요한 승인 여부를 심사 전에 확인해야 합니다. 외부 도구 사용이나 개인용이라는 사실만으로 정책 적합성을 단정하지 않습니다.

개인정보처리방침 게시, 브랜딩 검증, OAuth 범위 검증, YouTube API 정책 검토·감사는 서로 다른 확인 사항입니다. 이 사이트는 심사 통과를 보장하지 않습니다.
