# Endpoint-Security-Hardening
Windows 기반 보안 운영 및 침해사고 대응 자동화 스크립트 모음:

본 레포지토리는 엔드포인트 보안 관리, 취약점 탐지, 그리고 포렌식 데이터 수집을 자동화하기 위해 작성된 PowerShell 스크립트들을 포함하고 있습니다.
실무 환경에서의 보안 가시성 확보와 빠른 대응을 목적으로 합니다.

1. 스크립트별 상세 설명

① Log4j & Java 환경 분석 도구 (Detect-Log4j-And-Java.ps1)
용도: 인프라 내 Log4j 취약점(CVE-2021-44228) 노출 자산 전수 조사 및 Java 런타임 버전 관리.

주요 기능:

모든 드라이브 내 .jar, .war, .ear 파일 재귀적 탐색.

7-Zip 라이브러리를 활용해 압축 파일 내부의 JndiLookup.class 존재 여부 정밀 검사.

시스템 환경 변수, 레지스트리, 설치 경로를 통한 Java/JRE 설치 현황 수집.

결과물(CSV/JSON) 자동 백업 및 중앙 집중식 리포팅 지원.

② Microsoft Defender 월간 풀 스캔 자동화 (Intune_Defender_MonthlyFullScan_v5.ps1)
용도: Intune 환경 또는 독립 실행형 서버의 정기 정밀 검사 강제화.

주요 기능:

매월 첫째 주 토요일 새벽 2시 실행 스케줄러 등록.

CMD 래퍼(Wrapper)를 활용해 MpCmdRun.exe 호출 최적화 및 Fallback 로직 구현.

SYSTEM 권한 실행 및 최고 수준 권한(Highest Privilege) 할당으로 검사 신뢰성 확보.

③ RDP 로그인 보안 모니터링 (Login_Check_Script.ps1)
용도: 최근 RDP 접속 이력 분석을 통한 브루트 포스(Brute-force) 공격 탐지.

주요 기능:

Windows 이벤트 로그(ID: 4624, 4625) 기반 실시간 로그 파싱.

RDP(LogonType 10) 전용 필터링 및 성공/실패 Top 10 리스트 출력.

동일 IP 기반 반복 실패 이력을 요약하여 공격 의심 IP 자동 식별.

④ Osquery 기반 침해 지표 수집 파이프라인 (osquery-collect-pipeline.ps1)
용도: 침해사고 대응(IR) 시 엔드포인트에서 의심스러운 아티팩트 자동 수집 및 분석.

주요 기능:

osqueryi를 활용해 비정상 서비스, 임시 폴더 내 실행 파일, 외부 소켓 연결 정보 추출.

Heuristic Analysis: 서명되지 않은 바이너리, 최근 변경된 하이브(Hive) 파일 등을 자동 식별.

Evidence Collection: 의심 파일의 SHA-256 해시 생성 및 아티팩트 저장소로 자동 복사.

NDJSON 형식의 타임라인 리포트 생성으로 SIEM 연동 용이성 확보.

2. 기술스택 (Tech Stack)

Language: PowerShell 5.1 / 7+

Tools: Microsoft Defender, osquery, 7-Zip, Task Scheduler

OS: Windows Server 2016/2019/2022, Windows 10/11




