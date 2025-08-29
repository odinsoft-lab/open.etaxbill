# Contributing to Open eTaxBill

감사합니다! 아래 가이드를 따라 기여를 진행해 주세요.

## 기본 원칙
- 코드와 문서는 GPL-3.0-or-later에 따라 배포됩니다.
- 작은 변경이라도 이슈/PR 설명을 명확히 작성합니다.
- 기능 추가 시 테스트(가능한 범위), 문서를 함께 업데이트합니다.

## 브랜치 전략
- main/master: 안정화된 릴리스 브랜치
- feature/*: 기능 개발 브랜치
- fix/*: 버그 수정 브랜치
- docs/*: 문서만 변경

PR은 항상 최신 master를 기준으로 하며, 스쿼시 머지를 권장합니다.

## 이슈 등록
- 유형: bug / feature / docs / chore
- 재현 절차, 기대 결과, 실제 결과를 포함해 주세요.
- 스크린샷/로그/환경정보(Windows, .NET, SQL Server 버전)를 첨부하면 도움이 됩니다.

## 개발 환경
- Windows 10/11, Visual Studio 2019/2022
- .NET Framework 4.7.2 SDK
- SQL Server (Express 이상)

## 빌드 및 실행
- 솔루션: `open.etaxbill.sln`
- NuGet 복원 후 전체 빌드
- Certifier는 WinForms 앱으로 실행

## 코드 스타일
- C#: 기존 스타일을 따르고, 불필요한 포맷 변경은 피합니다.
- 네이밍: 기존 네임스페이스/파일 구조 유지
- 예외 처리: 사용자 친화적 메시지 + 로그 남기기

## 테스트
- 현재 프로젝트 특성상 통합 테스트가 중심입니다. 가능하다면 최소 단위테스트/스모크 테스트를 추가하세요.

## 보안/비밀정보
- 실제 인증서/비밀번호/연결문자열을 커밋하지 마세요.
- 예시 값은 placeholder로 대체합니다.

## 커밋 메시지
- 형식 예시: `feat(collector): 대량 업로드 성능 최적화`
- 접두사: feat, fix, docs, refactor, perf, test, chore

## 라이선스 동의
- PR 제출로, 제출된 코드가 GPL-3.0-or-later 하에 배포될 수 있음을 동의하는 것으로 간주됩니다.
