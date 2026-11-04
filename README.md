# Finesse Frontend

TETR.IO 매치 히스토리를 분석하고 AI 코멘터리를 보여 주는 웹 서비스 **Finesse**의 프론트엔드입니다.

> **팀 프로젝트 중 본인 담당 부분만 추출한 사본입니다.**
> 전체 프로젝트(백엔드 · LLM 서버 · 인프라 포함)는 원본 레포를 참고해 주세요.
>
> 원본 레포: https://github.com/SM-Finesse/Finesse

## 본인 역할

**호준수 — 프론트엔드 담당.** 이 레포의 `src/` 전체를 구현했습니다.

- 유저명 입력 화면(랜딩), 최근 검색, 결과 화면 헤더 검색
- 라이트 뷰 결과 화면과 헤비 뷰 8챕터 리포트, Recharts 기반 차트
- 전적 조회 API와 코멘트 API 연동, 헤비 코멘트 SSE 스트림 처리
- 지표 설명 카드, 지표 신뢰도 라벨, 단축키, 한국어 · 영어 문구 구조
- QA 결과 반영과 Vitest + Testing Library 테스트 작성

`Dockerfile`, `nginx/`, `.dockerignore`는 인프라 담당 팀원이 작성한 파일로, 함께 옮겨 두었습니다.

## 스택

React 19 · TypeScript 6 · Vite 8 · Tailwind CSS 4 · Recharts 3 · Vitest 5 + Testing Library

## 실행

Node **22.12 이상**이 필요합니다 (Vitest 5 · jsdom 30 요구사항).

```bash
npm ci              # 의존성 설치
npm run dev         # 개발 서버 → http://localhost:5173
npm test            # 테스트 1회 실행
npm run test:watch  # 저장할 때마다 테스트
npm run coverage    # 테스트 커버리지
npm run build       # 타입 검사(tsc -b) + 프로덕션 빌드
```

이 레포에는 백엔드가 없습니다. 실제 데이터를 보려면 [원본 레포](https://github.com/SM-Finesse/Finesse)의 백엔드를 띄워야 합니다. 개발 서버는 `/api` 요청을 `http://localhost:8080`으로 넘기며, 주소가 다르면 `.env.local`에 `VITE_API_PROXY_TARGET`을 지정합니다.

## 구조

```
src/
  pages/        화면 단위 (LandingPage = 유저명 입력, ReportPage = 결과 화면)
  components/   재사용 UI (UsernameForm, HeaderSearch, InfoPanel …), report/ = 리포트 화면
  api/          API 호출
  hooks/        전적 · 코멘트 조회(useStats, useLightComment, useHeavyComment), 단축키(useHotkeys)
  i18n/         한국어 · 영어 문구, useContext로 공유
  lib/          유저명 검증, 차트 계산 등 순수 로직
  index.css     Tailwind @theme 토큰 — 색 · 글꼴
```
