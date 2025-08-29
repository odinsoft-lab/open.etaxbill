# Open eTaxBill Roadmap

본 로드맵은 우선순위와 범위를 주기적으로 재검토합니다.

## 2025 H2
- Certifier UX 개선 및 오류 메시지 한글화 강화
- Channel 엔드포인트 구성 템플릿 제공(.config 샘플)
- Engine 빌드/배포 스크립트 정리(PostBuild → dotnet/msbuild task 문서화)
- DB 스키마 샘플/초기화 스크립트 문서화

## 2026 H1
- 엔진 서비스 호스트 템플릿(Windows Service/콘솔) 샘플 제공
- 로깅 표준화(예: ETW/Serilog 등)와 운영 가이드 작성
- 대량 업로드 최적화 가이드(collector)와 벤치마크 샘플

## 2026 H2
- 컨테이너 지원 가이드(Windows 기반) 문서화
- 다국어(ko/en) 문서 커버리지 확대
- 샘플 데이터/워크플로우 자동화(테스트 데이터셋)

## 탐색/연구 과제
- .NET 현대화 전환(가능 범위에서 .NET 6+로 마이그레이션) 타당성 분석
- 보안 강화를 위한 인증서/키 관리 전략 개선안
- 대체 전송 채널(REST) 검토 및 PoC

## 완료(역사)
- GPL-3.0-or-later 라이선스 정비 및 LICENSE/README 정리 (2025-08)
