# Open eTaxBill Tasks

우선순위는 P0 > P1 > P2 순입니다.

## P0 (핵심)
- [ ] `src/channel/App.config`의 엔드포인트 주소를 환경 변수/설정으로 분리하고 샘플 템플릿 추가
- [ ] `src/library/app.config`의 연결 문자열 예시 분리 및 보안 가이드(Secret 관리) 추가
- [ ] Certifier 예외 처리/로그 수집 개선(MainForm/Program 전역 핸들러 검토)

## P1 (중요)
- [ ] 엔진 서비스들(collector/mailer/provider/reporter/responsor/signer) 호스트 구성 가이드 초안
- [ ] PostBuild 산출물 복사 경로 문서화 및 VS 솔루션 설정 확인
- [ ] 설치/운영 가이드(INSTALL.md) 보강: 방화벽/포트, 권한, 의존성 상세

## P2 (개선)
- [ ] 스크린샷/다이어그램(아키텍처, 데이터 흐름) 추가
- [ ] 코드 주석/문서화 정리(영문 병기 확대)
- [ ] 샘플 데이터/테스트 워크플로우 제공

## 완료
- [x] README.md 깃헙 스타일 개편 (개요/구성/설정/빌드/실행/라이선스) (2025-08)
