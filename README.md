# UV 공부 (Windows)

UV는 Python 패키지 관리와 가상환경을 위한 빠르고 강력한 대체 도구입니다. pip, pip-tools, pipx, poetry, pyenv, twine, virtualenv 등 여러 Python 도구들을 통합하여 대체할 수 있는 올인원 관리 도구입니다.

## 주요 특징

- **초고속 성능**: Rust로 작성되어 매우 빠름
- **하드 링크 지원**: 동일한 패키지를 여러 환경에 설치해도 저장 공간을 효율적으로 사용
- **통합 관리**: 패키지 설치, 가상환경 생성, 빌드, 배포까지 모든 기능을 하나의 도구로 처리
- **자동 Python 설치**: 필요한 Python 버전을 자동으로 다운로드 및 설치

## 설치 방법

### 1. UV 설치
PowerShell을 통해 설치 (두 가지 방법 중 하나 선택):

```powershell
# 방법 1: 기본 설치
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"

# 방법 2: 실행 정책 우회 설치 (방법 1이 실패할 경우)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

> 참고:
> - `pip install uv`는 Python 패키지로 설치하는 방식이지만, UV의 본래 구현은 Rust 기반 바이너리입니다. 기능 및 성능 차이가 있으므로 위 설치 스크립트를 사용하는 것을 권장합니다.
> - 설치가 실패하는 경우 PowerShell을 관리자 권한으로 실행해보세요.
> - Windows 보안 경고가 나타날 경우 '예' 또는 '모두 예'를 선택하여 설치를 진행하세요.

## 기본 사용법

### 1. 가상환경 생성
```powershell
# 기본 가상환경 생성
uv venv .venv

# 특정 Python 버전으로 가상환경 생성
uv venv -p 3.13
```

> 참고: 지정한 Python 버전은 자동으로 다운로드되며, python-build-standalone을 통해 필요한 구성요소만 포함됩니다. IDLE, 문서 등은 포함되지 않으므로 별도 설치가 필요할 수 있습니다.

### 2. 패키지 설치
```powershell
# 단일 패키지 설치
uv pip install requests

# requirements.txt 파일로부터 패키지 설치
uv pip install -r requirements.txt

# 현재 디렉토리를 개발 모드로 설치 (editable install)
uv pip install -e .
```

### 3. 가상환경 활성화
```powershell
# PowerShell 및 CMD 공통
.venv\Scripts\activate
```

### 4. 패키지 관리
```powershell
# 설치된 패키지 목록 확인
uv pip list

# 패키지 업그레이드
uv pip install --upgrade package_name

# 패키지 제거
uv pip uninstall package_name
```

## UVX 사용법

uvx는 독립적인 Python CLI 도구(ex. black, ruff, httpie 등)를 간편하게 설치하고 실행할 수 있게 해주는 기능입니다.

```powershell
# black 포맷터 설치 및 실행
uvx black .

# ruff 설치 및 사용 예
uvx ruff check .
```

설치된 도구는 가상환경 없이도 즉시 실행 가능하며, 내부적으로 캐시되어 빠르게 재사용됩니다.

## 하드 링크 기능

UV는 Python 패키지를 설치할 때, 동일한 패키지를 여러 가상환경에 중복 설치하지 않고, 하드 링크를 통해 하나의 물리적 파일을 참조하게 합니다:

- 저장 공간 절약
- 설치 시간 단축
- 캐시 디렉토리 기본 위치: `%LOCALAPPDATA%\uv\pkgs`

## 문제 해결

### 1. 가상환경 활성화 오류
PowerShell 실행 정책 확인:
```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```
가상환경 경로가 올바른지 확인

### 2. 패키지 설치 실패
- 인터넷 연결 확인
- Python 버전 호환성 확인
- `--verbose` 옵션을 사용하여 자세한 오류 메시지 확인

### 3. UV 명령어 인식 안 됨
- 설치 후 uv 명령어가 작동하지 않는 경우, 설치 경로가 PATH에 포함되어 있는지 확인
- PowerShell을 재시작하거나, `Get-Command uv` 명령어로 경로를 확인

## 추가 리소스

- [UV 공식 문서](https://github.com/astral-sh/uv)
- [UV GitHub 저장소](https://github.com/astral-sh/uv)
- [Python 패키지 관리 가이드](https://packaging.python.org/)
