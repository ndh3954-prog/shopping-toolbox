# 부업 툴박스 (shopping-toolbox)

쿠팡/네이버쇼핑 셀러(농수산물 도매, 병행수입, 사입)를 위한 개인용 툴 대시보드.
단일 HTML 파일 + localStorage 기반, 서버 없음.

## 배포

- **배포 주소**: https://ndh3954-prog.github.io/shopping-toolbox/ (GitHub Pages, `main` 브랜치 `/ (root)`)
- 저장소: https://github.com/ndh3954-prog/shopping-toolbox
- 로컬 프로젝트 폴더: `~/shopping-toolbox` (main 파일은 `index.html`)
- 수정할 때: `~/shopping-toolbox/index.html`을 고쳐서 커밋 후 `git push` 하면 1~2분 내 위 주소에 자동 반영됨

## 현재 상태

- `index.html` — 지금까지 완성된 버전
- 대시보드에서 툴 2개 실행 가능:
  1. **상세페이지 제작기** — 플랫폼(쿠팡/네이버) x 카테고리(농수산물도매/병행수입/사입/기타)별 규칙이 내장된 프롬프트로 상세페이지 초안 생성
  2. **썸네일 생성기** — 스타일 프리셋 기반 이미지 프롬프트로 썸네일 이미지 생성

## 아키텍처 (중요)

- **AI 호출 방식**: 서버 없이, 브라우저에서 사용자의 API 키로 각 모델사(OpenAI, Google Gemini, xAI Grok)에 **직접 fetch 호출**.
  - API 키는 `localStorage`에만 저장 (키 이름: `toolbox_api_keys`)
  - 텍스트 생성 기록: `toolbox_detailpage_history` (최대 100개)
  - 썸네일 생성 기록: `toolbox_thumbnail_history` (최대 30개, base64라 용량 큼)
- **이 방식을 선택한 이유**: Claude Artifact(게시) 기능으로 배포하면 보안 정책상 외부 API(OpenAI/Gemini/Grok)로의 직접 네트워크 요청이 막혀서, 지금 설계한 "여러 모델을 직접 골라 쓰는" 구조가 작동하지 않음. 그래서 일반 정적 파일 + 자체 호스팅 방식으로 진행하기로 함.
- **알려진 제약**: 파일을 `file://`로 더블클릭해서 열면 브라우저에 따라 API 호출이 막힐 수 있음 → 로컬 서버(`python -m http.server` 등)나 실제 호스팅(GitHub Pages, Netlify, Vercel 등)에 올려서 사용 권장.

## 다음에 고려할 것

- ~~정적 호스팅 배포~~ → 완료 (GitHub Pages, 위 배포 주소 참고)
- 상세페이지 프롬프트 품질 다듬기 (카테고리별 규칙 실사용 테스트 필요)
- 이미지 생성 모델명은 세 회사 모두 자주 바뀌므로, 실제 테스트하면서 최신 모델 ID로 업데이트 필요
- 데이터 export/import (JSON) — 아직 미구현
- 세 번째 아이디어(AI세무사 상담+신뢰지수)는 별도 프로젝트로 독립 진행 예정

## 사용자 선호

- 단일 HTML 파일 + localStorage 선호
- 코딩 초보 — 설명은 쉽게, 변경사항은 파일 전체 교체 방식 선호
- 한국어로 소통
