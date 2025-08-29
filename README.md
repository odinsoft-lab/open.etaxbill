# Open eTaxBill (소스 공개 종료 안내)

본 저장소의 소스 코드는 더 이상 무상 라이선스로 제공되지 않습니다. 기존에 공개되었던 `src/` 하위 소스는 모두 제거되었으며, 오픈소스 이용은 중단되었습니다.

## 사용/도입 문의

서비스 도입, 기능 확장, 유지보수, 기술 지원이 필요하신 경우 아래로 연락해주세요.

- 회사: 오딘소프트 (Odinsoft)
- 이메일: help@odinsoft.co.kr
- 웹사이트: https://www.odinsoft.co.kr

요구사항(업무 범위, 기간, 예산, 환경 등)을 이메일로 간단히 남겨주시면 빠르게 안내드리겠습니다.

## 기존 문서 안내

- `docs/` 폴더에는 과거 기술 문서와 로드맵이 남아 있을 수 있으나, 현 정책과 기능은 별도 계약 기준으로 제공됩니다.
- `LICENSE.md`의 오픈소스 표기는 더 이상 유효하지 않습니다. 본 저장소의 잔여 파일은 안내 용도입니다.

## 법적 고지

본 저장소의 코드 및 문서를 무단으로 복제, 배포, 변경, 상업적 이용하는 행위를 금지합니다. 위반 시 관련 법령에 따라 책임을 물을 수 있습니다.

감사합니다.


---

# Open eTaxBill (안내)

국세청 전자세금계산서(ETAX) 연동을 위한 엔진/채널/인증 도구 모음입니다. 엔진은 전자세금계산서의 생성·서명·전송·응답·메일·수신 파이프라인을 담당하고, 채널은 각 엔진을 호출하는 WCF 클라이언트, Certifier는 KISA 전자세금계산서 인증 절차를 도와주는 WinForms 유틸리티입니다.

## 구성요소(Components)

- Engine(6 Services)
	- collector: 전자세금계산서 작성 및 DB 저장 (엑셀/ERP 대량 처리)
	- signer: 매출자 인증서로 전자세금계산서 서명/암호화
	- reporter: 국세청 보고(전송)
	- responsor: 국세청 처리결과 수신 및 DB 반영
	- mailer: ASP 사업자/매입자 메일 발송
	- provider: 타 ASP 수신 메일 파싱 및 매입 분 저장

- Channel: 엔진 호출용 WCF Channel 라이브러리 (`src/channel`)
- Certifier: 전자세금계산서 인증 보조 툴(WinForms) (`src/certifier`)

## 기술 스택(Tech Stack)

- .NET Framework 4.7.2, C#, WinForms, WCF
- Database: Microsoft SQL Server
- NuGet: BouncyCastle, Mono.Security, Npgsql, SharpZipLib, OdinSdk.*

## 프로젝트 구조(Project Structure)

```
open.etaxbill/
├─ open.etaxbill.sln
├─ INSTALL.md
├─ LICENSE.md
├─ README.md
└─ src/
	 ├─ certifier/                # 인증 유틸리티(WinForms)
	 │  ├─ App.config
	 │  ├─ etax.certifier.csproj
	 │  ├─ Program.cs, MainForm.*
	 │  ├─ dialogs/               # eTaxCreator, eTaxSigning 등 UI 폼
	 │  └─ work-folder/           # certkey, output 샘플 등
	 ├─ channel/                  # WCF 채널 라이브러리
	 │  ├─ App.config             # 엔드포인트/바인딩 설정
	 │  └─ etax.channel.csproj
	 └─ library/                  # 공통 유틸(Engine Library)
			├─ app.config             # DB 연결 문자열
			└─ etax.library.csproj
```

솔루션에는 추가로 engine/collector, mailer, provider, reporter, responsor, signer 프로젝트가 포함됩니다. 이들은 ETAX 파이프라인 각각의 역할을 담당하며, 별도의 호스트 또는 인프라에서 운영하도록 설계되어 있습니다.

## 사전 준비(Prerequisites)

- Windows 10/11, Visual Studio 2019 또는 2022 (.NET Framework 4.7.2 개발자 팩)
- Microsoft SQL Server (Express 이상)
- 방화벽/포트 공유 설정(운영 환경에서 WCF 엔드포인트 사용 시)
- 발급된 인증서 및 국세청/진흥원 공개키(필요 시 `src/certifier/work-folder/certkey` 활용)

## 설정(Configuration)

1) 데이터베이스 연결 문자열
- 파일: `src/library/app.config`
- 키: `OpenETaxBill.Engine.Library.Properties.Settings.ETAXConnectionString`
- 예시(값은 환경에 맞게 변경):

```
Data Source=YOUR_SQL_SERVER;Initial Catalog=ETAX;Persist Security Info=True;User ID=YOUR_ID;Password=YOUR_PASSWORD
```

2) WCF 엔드포인트(클라이언트)
- 파일: `src/channel/App.config`
- 각 endpoint의 address를 운영/테스트 환경 IP/도메인/포트에 맞게 수정하십시오. net.tcp 및 http 바인딩 모두 샘플이 포함되어 있습니다.

3) Certifier 설정
- 파일: `src/certifier/App.config`
- `WcfCollectorUrl` 등 앱 설정 값을 환경에 맞게 지정하십시오.

4) 포트/방화벽
- 운영 시 Windows 방화벽 인바운드 규칙에 필요한 포트(예: 8080, 8453, 8461 등)를 오픈해야 할 수 있습니다.

## 빌드(Build)

1) 솔루션 열기: `open.etaxbill.sln`
2) NuGet 패키지 복원 (Visual Studio 자동 복원 또는 솔루션 우클릭 → Restore)
3) 구성/플랫폼 선택(예: Release|Any CPU)
4) 전체 빌드

빌드 후 PostBuild 이벤트가 결과물을 솔루션 하위 `output/.../<ConfigurationName>` 경로로 복사합니다.

## 실행(Run)

- Certifier (WinForms): `OpenETaxBill.Certifier`를 시작하여 인증 절차(메뉴 순서)를 진행합니다.
- Engine/Channel: 실제 운영에서는 각 엔진을 서비스/호스트에 배치하고, 채널 라이브러리로 호출합니다. 엔드포인트/포트, 방화벽, 인증서 등을 환경에 맞게 구성해야 합니다.

## 의존성(Dependencies)

- BouncyCastle, Mono.Security, Npgsql, SharpZipLib, OdinSdk.eTaxBill, OdinSdk.OdinLib, OdinSdk.FormLib 등
- .NET Framework 4.7.2

## 라이선스(License)

본 프로젝트는 GPL-3.0-or-later로 배포됩니다. 자세한 내용은 `LICENSE.md`를 참고하세요.

## 참고 링크(Links)

- 전자세금계산서 인증(KISA): https://www.taxcerti.or.kr/etax/
- GNU GPLv3: https://www.gnu.org/licenses/gpl-3.0.html


