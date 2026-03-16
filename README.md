# KISA 주요정보통신기반시설 UNIX 서버 취약점 점검 스크립트

## 개요

본 스크립트는 KISA(한국인터넷진흥원)에서 발행한 「2026 주요정보통신기반시설 기술적 취약점 분석·평가 방법 상세가이드」에 따라 UNIX/Linux 서버의 보안 취약점 67개 항목을 자동으로 점검하고 리포트를 생성합니다.

## 주요 기능

### ✨ 핵심 기능
- **67개 보안 취약점 항목 완전 자동 점검** (중요도별 분류: 상/중/하)
- **현대적인 HTML 리포트** 및 텍스트 리포트 동시 생성
- **실시간 점검 진행률** 표시 및 색상 코드 활용
- **자동 취약점 조치 가이드** 제공 (중요도 "상" 항목)
- **확장된 설정 파일 검사** (커스텀 설정 파일 포함)

### 🔍 고급 점검 기능
- **SSH 설정 다중 파일 검사** (`/etc/ssh/sshd_config.d/*.conf` 포함)
- **세션 타임아웃 다중 위치 검사** (TMOUT, SSH ClientAlive 등)
- **심볼릭 링크 인식** 및 실제 파일 권한 검사
- **서비스 상태 정확한 판정** (systemd 기반)
- **권한 검사 로직 개선** (숫자/문자열 권한 모두 지원)

### 📊 리포트 기능
- **반응형 HTML 디자인** (모바일 지원)
- **점검 결과 요약** (상단 배치로 한눈에 파악)
- **📋 인터랙티브 체크리스트** (클릭으로 상세 결과 이동)
- **카테고리별 구분** 및 중요도별 색상 표시
- **상세한 조치 방법** (취약 항목 발견 시 자동 표시)
- **줄바꿈 처리 개선** (텍스트/HTML 모두 정확한 포맷팅)
- **줄바꿈 처리 개선** (텍스트/HTML 모두 정확한 포맷팅)

## 지원 운영체제

- Rocky Linux 8.x, 9.x ✅
- CentOS 7.x, 8.x ✅  
- RHEL 7.x, 8.x, 9.x ✅
- Ubuntu 18.04, 20.04, 22.04 ✅
- Debian 10, 11, 12 ✅

## 점검 항목 (67개)

### 분류별 항목 수
- 1. 계정 관리: U-01 ~ U-13 (13개)
- 2. 파일 및 디렉터리 관리: U-14 ~ U-33 (20개)
- 3. 서비스 관리: U-34 ~ U-63 (30개)
- 4. 패치 관리: U-64 (1개)
- 5. 로그 관리: U-65 ~ U-67 (3개)

### 중요도별 항목 수
- 상 (High): 44개
- 중 (Medium): 16개
- 하 (Low): 7개

### 1. 계정 관리 (U-01 ~ U-13) - 13개 항목
- U-01 (상): root 계정 원격 접속 제한
- U-02 (상): 비밀번호 관리정책 설정
- U-03 (상): 계정 잠금 임계값 설정
- U-04 (상): 비밀번호 파일 보호
- U-05 (상): root 이외의 UID가 '0' 금지
- U-06 (상): 사용자 계정 su 기능 제한
- U-07 (하): 불필요한 계정 제거
- U-08 (중): 관리자 그룹에 최소한의 계정 포함
- U-09 (하): 계정이 존재하지 않는 GID 금지
- U-10 (중): 동일한 UID 금지
- U-11 (하): 사용자 Shell 점검
- U-12 (하): 세션 종료 시간 설정
- U-13 (중): 안전한 비밀번호 암호화 알고리즘 사용

### 2. 파일 및 디렉터리 관리 (U-14 ~ U-33) - 20개 항목
- U-14 (상): root 홈, 패스 디렉터리 권한 및 패스 설정
- U-15 (상): 파일 및 디렉터리 소유자 설정
- U-16 (상): /etc/passwd 파일 소유자 및 권한 설정
- U-17 (상): 시스템 시작 스크립트 권한 설정
- U-18 (상): /etc/shadow 파일 소유자 및 권한 설정
- U-19 (상): /etc/hosts 파일 소유자 및 권한 설정
- U-20 (상): /etc/(x)inetd.conf 파일 소유자 및 권한 설정
- U-21 (상): /etc/(r)syslog.conf 파일 소유자 및 권한 설정
- U-22 (상): /etc/services 파일 소유자 및 권한 설정
- U-23 (상): SUID, SGID, Sticky bit 설정 파일 점검
- U-24 (상): 사용자, 시스템 환경변수 파일 소유자 및 권한 설정
- U-25 (상): world writable 파일 점검
- U-26 (상): /dev에 존재하지 않는 device 파일 점검
- U-27 (상): $HOME/.rhosts, hosts.equiv 사용 금지
- U-28 (상): 접속 IP 및 포트 제한
- U-29 (하): hosts.lpd 파일 소유자 및 권한 설정
- U-30 (중): UMASK 설정 관리
- U-31 (중): 홈 디렉토리 소유자 및 권한 설정
- U-32 (중): 홈 디렉토리로 지정한 디렉토리의 존재 관리
- U-33 (하): 숨겨진 파일 및 디렉토리 검색 및 제거

### 3. 서비스 관리 (U-34 ~ U-63) - 30개 항목
- U-34 (상): Finger 서비스 비활성화
- U-35 (상): 공유 서비스에 대한 익명 접근 제한 설정
- U-36 (상): r계열 서비스 비활성화
- U-37 (상): crontab 설정파일 권한 설정
- U-38 (상): DoS 공격에 취약한 서비스 비활성화
- U-39 (상): 불필요한 NFS 서비스 비활성화
- U-40 (상): NFS 접근 통제
- U-41 (상): 불필요한 automountd 제거
- U-42 (상): 불필요한 RPC 서비스 비활성화
- U-43 (상): NIS, NIS+ 점검
- U-44 (상): tftp, talk 서비스 비활성화
- U-45 (상): 메일 서비스 버전 점검
- U-46 (상): 일반 사용자의 메일 서비스 실행 방지
- U-47 (상): 스팸 메일 릴레이 제한
- U-48 (중): expn, vrfy 명령어 제한
- U-49 (상): DNS 보안 버전 패치
- U-50 (상): DNS Zone Transfer 설정
- U-51 (중): DNS 서비스의 취약한 동적 업데이트 설정 금지
- U-52 (중): Telnet 서비스 비활성화
- U-53 (하): FTP 서비스 정보 노출 제한
- U-54 (중): 암호화되지 않는 FTP 서비스 비활성화
- U-55 (중): FTP 계정 Shell 제한
- U-56 (하): FTP 서비스 접근 제어 설정
- U-57 (중): Ftpusers 파일 설정
- U-58 (중): 불필요한 SNMP 서비스 구동 점검
- U-59 (상): 안전한 SNMP 버전 사용
- U-60 (중): SNMP Community String 복잡성 설정
- U-61 (상): SNMP Access Control 설정
- U-62 (하): 로그인 시 경고 메시지 설정
- U-63 (중): sudo 명령어 접근 관리

### 4. 패치 관리 (U-64) - 1개 항목
- U-64 (상): 주기적 보안 패치 및 벤더 권고사항 적용

### 5. 로그 관리 (U-65 ~ U-67) - 3개 항목
- U-65 (중): NTP 및 시각 동기화 설정
- U-66 (중): 정책에 따른 시스템 로깅 설정
- U-67 (중): 로그 디렉터리 소유자 및 권한 설정

## 사용 방법

### 1. 스크립트 준비

```bash
# 실행 권한 부여
chmod +x kisa_unix_vulnerability_check.sh

# Windows에서 작성된 경우 줄바꿈 변환
sed -i 's/\r$//' kisa_unix_vulnerability_check.sh
```

### 2. 기본 실행 (일반 사용자)

```bash
./kisa_unix_vulnerability_check.sh
```

⚠️ **주의**: 일부 점검 항목은 제한적으로 동작할 수 있습니다.

### 3. 권장 실행 (root 권한) ⭐

```bash
sudo bash kisa_unix_vulnerability_check.sh
```

✅ **권장**: 모든 점검 항목을 정확하게 수행하려면 root 권한이 필요합니다.

### 4. 실행 화면 예시

```
================================================================================
  KISA 주요정보통신기반시설 UNIX 서버 취약점 점검 스크립트
  버전: 2.0 (2026 가이드라인 정확 반영)
  점검 항목: 67개
  - 1. 계정 관리: U-01 ~ U-13 (13개)
  - 2. 파일 및 디렉터리 관리: U-14 ~ U-33 (20개)
  - 3. 서비스 관리: U-34 ~ U-63 (30개)
  - 4. 패치 관리: U-64 (1개)
  - 5. 로그 관리: U-65 ~ U-67 (3개)
================================================================================

점검을 시작합니다...

[1/5] 계정 관리 점검 중 (13개 항목)...
  U-01: root 계정 원격 접속 제한... 완료
  U-02: 비밀번호 관리정책 설정... 완료
  ...

점검 결과 요약:
  전체 점검 항목: 67
  양호: 58
  취약: 0
  경고/점검필요: 9
```

### 5. 생성되는 리포트 파일

실행 완료 후 다음 파일들이 생성됩니다:

```
📄 KISA_Unix_Vulnerability_Report_20260316_152721.txt  # 텍스트 리포트
🌐 KISA_Unix_Vulnerability_Report_20260316_152721.html # HTML 리포트
```

## 리포트 내용

### 📊 HTML 리포트 특징

- **현대적인 반응형 디자인** (PC/모바일 모두 지원)
- **그라데이션 배경** 및 카드 스타일 레이아웃
- **점검 결과 요약** (시스템 정보 바로 아래 배치)
- **호버 효과** 및 부드러운 애니메이션
### 📋 점검 결과 상태

| 상태 | 의미 | 색상 | 조치 필요성 |
|------|------|------|-------------|
| **양호** | 보안 설정이 적절하게 구성됨 | 🟢 녹색 | 조치 불필요 |
| **취약** | 보안 취약점이 발견되어 조치 필요 | 🔴 빨강 | **즉시 조치 필요** |
| **경고/점검필요** | 수동 검토 필요 또는 환경별 판단 | 🟡 노랑 | 검토 후 판단 |

### 🎯 인터랙티브 체크리스트 기능

HTML 리포트에는 **클릭 가능한 체크리스트**가 포함되어 있어 효율적인 점검 결과 검토가 가능합니다:

#### 📋 체크리스트 특징
- **전체 67개 항목** 한눈에 보기 (U-01 ~ U-67)
- **카테고리별 그룹화** (계정관리, 파일및디렉터리, 서비스관리, 패치관리, 로그관리)
- **상태별 아이콘 표시**:
  - ✅ **양호** (녹색 배경)
  - ❌ **취약** (빨간색 배경)  
  - ⚠️ **경고/점검필요** (노란색 배경)
- **클릭으로 상세 이동**: 항목 클릭 시 해당 상세 결과로 부드럽게 스크롤
- **반응형 디자인**: PC/모바일 모든 환경에서 최적화된 표시

#### 🖱️ 사용 방법
1. HTML 리포트 열기
2. 상단의 **"📋 점검 항목 체크리스트"** 섹션 확인
### 📁 리포트 구성

1. **시스템 정보** (호스트명, OS 버전, 점검 일시, 점검자)
2. **📊 점검 결과 요약** (전체/양호/취약/경고 개수)
3. **📋 점검 항목 체크리스트** (U-01~U-67 전체 항목, 클릭으로 상세 이동)
4. **카테고리별 상세 점검 결과** (67개 항목)
   - 계정 관리 (13개)
   - 파일 및 디렉터리 관리 (20개) 
   - 서비스 관리 (30개)
   - 패치 관리 (1개)
   - 로그 관리 (3개)
HTML 리포트에는 **클릭 가능한 체크리스트**가 포함되어 있어 효율적인 점검 결과 검토가 가능합니다:

#### 📋 체크리스트 특징
- **전체 67개 항목** 한눈에 보기 (U-01 ~ U-67)
- **카테고리별 그룹화** (계정관리, 파일및디렉터리, 서비스관리, 패치관리, 로그관리)
- **상태별 아이콘 표시**:
  - ✅ **양호** (녹색 배경)
  - ❌ **취약** (빨간색 배경)  
  - ⚠️ **경고/점검필요** (노란색 배경)
- **클릭으로 상세 이동**: 항목 클릭 시 해당 상세 결과로 부드럽게 스크롤
- **반응형 디자인**: PC/모바일 모든 환경에서 최적화된 표시

#### 🖱️ 사용 방법
1. HTML 리포트 열기
2. 상단의 **"📋 점검 항목 체크리스트"** 섹션 확인
### 📁 리포트 구성

1. **시스템 정보** (호스트명, OS 버전, 점검 일시, 점검자)
2. **📊 점검 결과 요약** (전체/양호/취약/경고 개수)
3. **📋 점검 항목 체크리스트** (U-01~U-67 전체 항목, 클릭으로 상세 이동)
4. **카테고리별 상세 점검 결과** (67개 항목)
   - 계정 관리 (13개)
   - 파일 및 디렉터리 관리 (20개) 
   - 서비스 관리 (30개)
   - 패치 관리 (1개)
   - 로그 관리 (3개)리스트 기능

HTML 리포트에는 **클릭 가능한 체크리스트**가 포함되어 있어 효율적인 점검 결과 검토가 가능합니다:

#### 📋 체크리스트 특징
- **전체 67개 항목** 한눈에 보기 (U-01 ~ U-67)
- **카테고리별 그룹화** (계정관리, 파일및디렉터리, 서비스관리, 패치관리, 로그관리)
- **상태별 아이콘 표시**:
  - ✅ **양호** (녹색 배경)
  - ❌ **취약** (빨간색 배경)  
  - ⚠️ **경고/점검필요** (노란색 배경)
- **클릭으로 상세 이동**: 항목 클릭 시 해당 상세 결과로 부드럽게 스크롤
- **반응형 디자인**: PC/모바일 모든 환경에서 최적화된 표시

#### 🖱️ 사용 방법
1. HTML 리포트 열기
2. 상단의 **"📋 점검 항목 체크리스트"** 섹션 확인
3. 관심 있는 항목(예: ❌ 취약 항목) 클릭
4. 해당 항목의 상세 점검 결과 및 조치 방법 자동 이동

#### 💡 활용 팁
- **취약 항목 우선 검토**: 빨간색(❌) 항목부터 클릭하여 즉시 조치
- **카테고리별 점검**: 특정 영역(예: 서비스관리) 집중 검토
- **모바일에서도 편리**: 터치로 쉽게 네비게이션 가능
| **경고/점검필요** | 수동 검토 필요 또는 환경별 판단 | 🟡 노랑 | 검토 후 판단 |

### 🛠️ 자동 조치 가이드

**중요도 "상" 항목**이 **취약**으로 판정될 경우, 리포트에 **상세한 조치 방법**이 자동으로 포함됩니다:

```
⚠️ 조치 방법
1. SSH 설정 파일 수정
   sudo vi /etc/ssh/sshd_config
   PermitRootLogin no

2. SSH 서비스 재시작
   sudo systemctl restart sshd

3. 설정 확인
   sudo sshd -t
```
### 📁 리포트 구성

1. **시스템 정보** (호스트명, OS 버전, 점검 일시, 점검자)
2. **📊 점검 결과 요약** (전체/양호/취약/경고 개수)
3. **📋 점검 항목 체크리스트** (U-01~U-67 전체 항목, 클릭으로 상세 이동)
4. **카테고리별 상세 점검 결과** (67개 항목)
   - 계정 관리 (13개)
   - 파일 및 디렉터리 관리 (20개) 
   - 서비스 관리 (30개)
   - 패치 관리 (1개)
   - 로그 관리 (3개)
   - 로그 관리 (3개)

## 고급 기능

### 🔧 확장된 설정 파일 검사

스크립트는 기본 설정 파일뿐만 아니라 **커스텀 설정 파일**도 자동으로 검사합니다:

#### SSH 설정 (U-01, U-12)
```bash
/etc/ssh/sshd_config              # 기본 설정
/etc/ssh/sshd_config.d/*.conf     # 추가 설정 파일들
/etc/pam.d/sshd                   # PAM SSH 모듈
```

#### 세션 타임아웃 (U-12)
```bash
/etc/profile                      # 시스템 전역 프로파일
/etc/bashrc, /etc/bash.bashrc     # Bash 설정
/etc/profile.d/*.sh               # 프로파일 확장 스크립트
~/.bashrc, ~/.profile             # 사용자별 설정
```

### 🔍 정확한 권한 검사

- **심볼릭 링크 인식**: `/etc/rc.local` → `/etc/rc.d/rc.local` 실제 파일 검사
- **숫자/문자열 권한 모두 지원**: `000`, `0`, `----------` 모두 정확히 판정
- **소유자 검증**: `root:root` 소유자 확인

### ⚡ 성능 최적화

- **샘플링 검사**: `/etc/init.d/` 전체 대신 상위 5개 파일만 검사
- **효율적인 서비스 검사**: `systemctl` 기반 정확한 상태 확인
- **메모리 효율적인 파일 처리**: 대용량 로그 파일 안전 처리

## 시스템 요구사항

### 필수 요구사항
- **운영체제**: Rocky Linux, CentOS, RHEL, Ubuntu, Debian
- **Shell**: Bash 4.0 이상
- **권한**: 일반 사용자 (권장: root)
- **디스크 공간**: 최소 10MB (리포트 파일용)

### 권장 요구사항
- **메모리**: 최소 512MB RAM
- **CPU**: 1 Core 이상
- **네트워크**: 인터넷 연결 (패키지 정보 확인용)

### 필요한 명령어
대부분의 명령어는 기본 설치되어 있지만, 일부 시스템에서는 추가 설치가 필요할 수 있습니다:

```bash
# Rocky Linux / CentOS / RHEL
sudo dnf install -y audit policycoreutils-python-utils net-tools

# Ubuntu / Debian  
sudo apt install -y auditd policycoreutils net-tools
```

## 주의사항 및 제한사항

### ⚠️ 중요 주의사항

1. **자동화 도구의 한계**: 본 스크립트는 자동화된 점검 도구이며, **일부 항목은 수동 검토가 필요**합니다.

2. **참고용 결과**: 점검 결과는 **참고용**이며, 실제 보안 조치는 **조직의 보안 정책**에 따라 수행해야 합니다.

3. **테스트 환경 검증**: **프로덕션 환경에서 실행 전** 테스트 환경에서 먼저 검증하는 것을 **강력히 권장**합니다.

4. **시스템 부하**: 일부 점검 항목(파일 검색 등)은 **시스템 부하**를 발생시킬 수 있으므로 **업무 시간 외 실행**을 권장합니다.

5. **권한 문제**: Windows에서 작성된 스크립트는 **줄바꿈 문제**가 있을 수 있으니 `sed -i 's/\r$//' *.sh` 명령으로 변환하세요.

### 🔒 보안 고려사항

- **로그 기록**: 점검 과정이 시스템 로그에 기록될 수 있습니다.
- **임시 파일**: `/tmp` 디렉터리에 임시 파일이 생성되며 자동으로 정리됩니다.
- **네트워크 접근**: 일부 점검에서 로컬 네트워크 정보를 확인합니다.

### 📋 수동 검토 필요 항목

다음 항목들은 **환경별 특성**을 고려한 **수동 검토**가 필요합니다:

- **U-07**: 불필요한 계정 제거 (비즈니스 요구사항 고려)
- **U-08**: 관리자 그룹 구성원 (조직 정책 고려)  
- **U-23**: SUID/SGID 파일 (애플리케이션 요구사항 고려)
- **U-33**: 숨겨진 파일 (정당한 설정 파일 구분)

## 문제 해결

### 🚫 일반적인 오류 및 해결방법

#### 1. 권한 오류
```bash
# 오류: Permission denied
chmod +x kisa_unix_vulnerability_check.sh
sudo ./kisa_unix_vulnerability_check.sh
```

#### 2. 명령어 없음 오류
```bash
# Rocky Linux / CentOS
sudo dnf install -y audit net-tools policycoreutils-python-utils

# Ubuntu / Debian
sudo apt update
sudo apt install -y auditd net-tools policycoreutils
```

#### 3. 줄바꿈 문제 (Windows → Linux)
```bash
# Windows에서 작성된 파일의 줄바꿈 변환
sed -i 's/\r$//' kisa_unix_vulnerability_check.sh
dos2unix kisa_unix_vulnerability_check.sh  # dos2unix 설치된 경우
```

#### 4. HTML 파일 권한 문제
```bash
# HTML 리포트 파일 권한 복구
sudo chown $(whoami):$(whoami) *.html
chmod 644 *.html
```

#### 5. 디스크 공간 부족
```bash
# 이전 리포트 파일 정리
rm -f KISA_Unix_Vulnerability_Report_*.txt
rm -f KISA_Unix_Vulnerability_Report_*.html

# 디스크 사용량 확인
df -h .
```

### 🐛 디버깅 모드

스크립트 실행 중 문제가 발생하면 디버그 모드로 실행하세요:

```bash
# 디버그 모드 실행
bash -x ./kisa_unix_vulnerability_check.sh

# 특정 함수만 디버그
bash -c 'set -x; source ./kisa_unix_vulnerability_check.sh; check_account_management'
```

## 취약점 조치 가이드

### 🛡️ 주요 취약점 조치 방법

#### 🔐 root 원격 접속 제한 (U-01)

```bash
# 1. SSH 설정 수정
sudo vi /etc/ssh/sshd_config
# 또는 추가 설정 파일 사용
sudo vi /etc/ssh/sshd_config.d/99-security.conf

# 설정 내용
PermitRootLogin no

# 2. SSH 서비스 재시작
sudo systemctl restart sshd

# 3. 설정 확인
sudo sshd -t
sudo systemctl status sshd
```

#### 🔑 비밀번호 복잡성 설정 (U-02)

```bash
# 1. Rocky Linux 8+ 비밀번호 품질 설정
sudo vi /etc/security/pwquality.conf

# 설정 내용
minlen = 8          # 최소 길이
dcredit = -1        # 숫자 최소 1개
ucredit = -1        # 대문자 최소 1개  
lcredit = -1        # 소문자 최소 1개
ocredit = -1        # 특수문자 최소 1개
minclass = 3        # 최소 문자 클래스 수
maxrepeat = 2       # 연속 동일 문자 제한

# 2. 구버전 시스템 PAM 설정
sudo vi /etc/pam.d/system-auth
password requisite pam_pwquality.so retry=3 minlen=8 dcredit=-1 ucredit=-1 lcredit=-1 ocredit=-1

# 3. 설정 테스트
sudo pwscore <<< 'TestPassword123!'
```

#### 🔒 계정 잠금 설정 (U-03)

```bash
# 1. Rocky Linux 8+ faillock 설정
sudo authselect enable-feature with-faillock
sudo authselect apply-changes

# 2. faillock 상세 설정
sudo vi /etc/security/faillock.conf

# 설정 내용
deny = 5            # 5회 실패 시 잠금
unlock_time = 600   # 10분 후 자동 해제
fail_interval = 900 # 실패 카운트 리셋 시간
root_unlock_time = 60  # root 계정 잠금 시간

# 3. 구버전 시스템 PAM 설정
sudo vi /etc/pam.d/system-auth
auth required pam_faillock.so preauth deny=5 unlock_time=600
auth required pam_faillock.so authfail deny=5 unlock_time=600
account required pam_faillock.so

# 4. 잠금 상태 확인 및 해제
sudo faillock --user username
sudo faillock --user username --reset
```

#### 🔥 방화벽 설정 (U-28)

```bash
# 1. firewalld 활성화
sudo systemctl enable --now firewalld

# 2. 기본 서비스 허용
sudo firewall-cmd --permanent --add-service=ssh
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https

# 3. 특정 IP만 SSH 허용
sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="192.168.1.0/24" service name="ssh" accept'
sudo firewall-cmd --permanent --remove-service=ssh

# 4. 설정 적용 및 확인
sudo firewall-cmd --reload
sudo firewall-cmd --list-all
```

#### 📊 시스템 감사 설정 (로그 관리)

```bash
# 1. auditd 활성화
sudo systemctl enable --now auditd

# 2. 감사 규칙 설정
sudo vi /etc/audit/rules.d/audit.rules

# 주요 감사 규칙
-w /etc/passwd -p wa -k identity
-w /etc/group -p wa -k identity
-w /etc/shadow -p wa -k identity
-w /etc/sudoers -p wa -k actions
-w /var/log/faillog -p wa -k logins
-w /var/log/lastlog -p wa -k logins
#### ✨ 새로운 기능
- **현대적인 HTML 리포트** (반응형 디자인, 그라데이션 배경)
- **📋 인터랙티브 체크리스트** (U-01~U-67 전체 항목, 클릭으로 상세 이동)
- **자동 조치 가이드** (중요도 "상" 취약 항목)
- **확장된 설정 파일 검사** (SSH, 세션 타임아웃 등)
- **점검 결과 요약** (상단 배치)
sudo ausearch -k identity
sudo aureport --summary
```

#### ⏰ 세션 타임아웃 설정 (U-12)

```bash
# 1. 시스템 전역 TMOUT 설정
sudo vi /etc/profile.d/timeout.sh

# 설정 내용
export TMOUT=600  # 10분 타임아웃
readonly TMOUT

# 2. SSH ClientAlive 설정
sudo vi /etc/ssh/sshd_config.d/99-timeout.conf

# 설정 내용
ClientAliveInterval 300    # 5분마다 확인
ClientAliveCountMax 2      # 2회 무응답 시 연결 종료

#### ✨ 새로운 기능
- **현대적인 HTML 리포트** (반응형 디자인, 그라데이션 배경)
- **📋 인터랙티브 체크리스트** (U-01~U-67 전체 항목, 클릭으로 상세 이동)
- **자동 조치 가이드** (중요도 "상" 취약 항목)
- **확장된 설정 파일 검사** (SSH, 세션 타임아웃 등)
- **점검 결과 요약** (상단 배치)

주요 보안 설정을 한번에 적용하는 스크립트:

```bash
#!/bin/bash
# KISA 보안 강화 스크립트

echo "KISA 보안 설정 적용 중..."

# SSH 보안 강화
sudo tee /etc/ssh/sshd_config.d/99-kisa-security.conf << EOF
PermitRootLogin no
PasswordAuthentication yes
PubkeyAuthentication yes
ClientAliveInterval 300
ClientAliveCountMax 2
MaxAuthTries 3
EOF

# 방화벽 활성화
sudo systemctl enable --now firewalld
sudo firewall-cmd --permanent --add-service=ssh
sudo firewall-cmd --reload

# 감사 시스템 활성화
sudo systemctl enable --now auditd

# 세션 타임아웃 설정
sudo tee /etc/profile.d/kisa-timeout.sh << EOF
export TMOUT=600
readonly TMOUT
EOF

# 서비스 재시작
sudo systemctl restart sshd

echo "KISA 보안 설정 완료!"
```

## 버전 정보 및 업데이트

### 📋 현재 버전
- **버전**: 2.0
- **최종 수정일**: 2026-03-16
- **점검 항목**: 67개 (완전 구현)
- **지원 OS**: Rocky Linux, CentOS, RHEL, Ubuntu, Debian

#### ✨ 새로운 기능
- **현대적인 HTML 리포트** (반응형 디자인, 그라데이션 배경)
- **📋 인터랙티브 체크리스트** (U-01~U-67 전체 항목, 클릭으로 상세 이동)
- **자동 조치 가이드** (중요도 "상" 취약 항목)
- **확장된 설정 파일 검사** (SSH, 세션 타임아웃 등)
- **점검 결과 요약** (상단 배치)

#### 🔧 개선된 기능  
- **심볼릭 링크 처리** (실제 파일 권한 검사)
- **권한 검사 로직** (숫자/문자열 모두 지원)
- **줄바꿈 처리** (HTML/텍스트 정확한 포맷팅)
- **성능 최적화** (샘플링 검사, 효율적인 파일 처리)

#### 🐛 수정된 버그
- U-04/U-18 shadow 파일 권한 오판 수정
- U-17 심볼릭 링크 권한 오류 수정  
- U-63 NOPASSWD 주석 오탐 수정
- HTML 리포트 줄바꿈 문제 수정

### 🔄 업데이트 방법

```bash
# 1. 기존 스크립트 백업
cp kisa_unix_vulnerability_check.sh kisa_unix_vulnerability_check.sh.backup

# 2. 새 버전 다운로드 (예시)
wget https://example.com/kisa_unix_vulnerability_check.sh

# 3. 실행 권한 부여
chmod +x kisa_unix_vulnerability_check.sh

# 4. 줄바꿈 변환 (필요시)
sed -i 's/\r$//' kisa_unix_vulnerability_check.sh
```

## 라이선스 및 법적 고지

### 📜 라이선스
본 스크립트는 **KISA 가이드라인**을 기반으로 작성되었으며, **교육 및 보안 점검 목적**으로 자유롭게 사용할 수 있습니다.

### ⚖️ 면책 조항
- 본 도구는 **참고용**이며, 사용으로 인한 **시스템 장애나 보안 사고**에 대해 개발자는 책임지지 않습니다.
- **프로덕션 환경** 적용 전 **충분한 테스트**를 수행하시기 바랍니다.
- **조직의 보안 정책**과 **컴플라이언스 요구사항**을 우선적으로 고려하세요.

### 🏢 상업적 이용
- **비상업적 목적**: 자유 사용 가능
- **상업적 목적**: 별도 협의 필요

## 참고 자료 및 문의

### 📚 공식 참고 자료
- **KISA 주요정보통신기반시설 기술적 취약점 분석·평가 방법 상세가이드 (2026)**
- **KISA 홈페이지**: https://www.kisa.or.kr
- **보안 가이드**: https://www.kisa.or.kr/2060301
- **취약점 신고**: https://www.krcert.or.kr

### 🔗 관련 도구 및 자료
- **CIS Benchmarks**: https://www.cisecurity.org/cis-benchmarks
- **NIST Cybersecurity Framework**: https://www.nist.gov/cyberframework
- **OWASP Security Guidelines**: https://owasp.org

### 📞 문의 및 지원

#### 기술 지원
- **시스템 관리자** 또는 **보안 담당자**에게 문의
- **조직 내 IT 헬프데스크** 활용

#### 보안 관련 문의  
- **KISA 인터넷보안센터**: 국번없이 118
- **보안 취약점 신고**: cert@krcert.or.kr

#### 개선 제안
보안 점검 스크립트 개선 제안이나 버그 리포트는 조직 내 보안 담당 부서를 통해 전달해 주시기 바랍니다.

---

## 📋 체크리스트

### 실행 전 확인사항
- [ ] 스크립트 실행 권한 확인 (`chmod +x`)
- [ ] 줄바꿈 변환 완료 (`sed -i 's/\r$//'`)  
- [ ] 디스크 공간 확인 (최소 10MB)
- [ ] 테스트 환경에서 사전 검증 완료
- [ ] 업무 시간 외 실행 계획 수립

### 실행 후 확인사항
- [ ] 리포트 파일 생성 확인 (TXT, HTML)
- [ ] 취약 항목 조치 계획 수립
- [ ] 수동 검토 항목 별도 점검
- [ ] 정기 점검 일정 수립
- [ ] 결과 보고서 작성 및 보고

**🎯 목표**: 모든 항목이 **양호** 상태가 되도록 지속적인 보안 관리를 수행하세요!
