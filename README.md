# Git & GitHub 정리

<br>

# 1. 로컬 저장소 (git)

## 1.1 로컬 저장소 초기화
```bash
git init
```

<br>

## 1.2 로컬 저장소에 원격 저장소 지정
```bash
git remote add origin 원격저장소주소.git
```

<br>

## 1.3 브랜치 통합
```bash
git branch -M 브랜치명
```

<br>

## 1.4 토큰 등록
1. `.git/config` 파일 열기
2. `[remote "origin"]` 항목의 url 값 수정
   ```
   url = http://본인계정:토큰@github.com/깃허브레포지터리주소.git
   ```

<br>

## 1.5 작업 목록에 추가
```bash
git add 작업한파일명
git add .
```

<br>

## 1.6 커밋
```bash
git commit -m "커밋메시지"
```

<br>

## 1.7 깃허브에 배포
```bash
git push -u origin main
```

<br><br>

# 2. 원격 저장소 작업 (git & GitHub)

## 2.1 git clone

### 기본 복제
```bash
git clone 레포지터리주소
```

<br>

### 특정 브랜치만 복제
```bash
git clone -b 브랜치명 --single-branch 레포지터리주소.git
```

<br>

### 여러 브랜치가 존재하는 경우 (예: main / dev / design)
```bash
git clone 레포지터리주소
cd 레포지터리명

# 각 브랜치로 이동하여 확인
git checkout dev
git checkout main
git checkout design

# 작업할 브랜치로 통합
git branch -M dev
```

<br>

## 2.2 git fork

> GitHub 상에서 타인의 레포지터리를 본인 계정으로 복사하는 기능

1. 복사할 레포지터리 페이지 접속
2. 우측 상단 **[Fork]** 버튼 클릭
3. 본인 계정으로 레포지터리가 복사됨

> ⚠️ **주의사항**
> - 본인 계정으로 로그인된 상태여야 함
> - 자신의 레포지터리는 fork 불가

<br>

## 2.3 git pull

### 기본 사용법
```bash
git pull origin 브랜치명
```

<br>

### 원격 저장소 내용 가져오기 (전체 흐름)
```bash
git init
git remote add origin 깃허브레포지터리주소.git
git pull 깃허브레포지터리주소.git
git branch -M 브랜치명
git pull origin 브랜치명
```

<br><br>

# 3. Pull Request (PR)

> GitHub에서 특정 브랜치의 변경 사항을 다른 브랜치에 병합(merge)해 달라고 요청하는 기능  
> 팀 리더(main 관리자)가 코드를 검토하고, 승인·수정 요청·의견을 남기는 **협업 및 품질 관리 창구**로 활용된다.

<br>

## 3.1 기본 개념: 브랜치 구조

```
main
├── frontend
└── backend
```

- `main` → `frontend` / `backend` 방향으로 PR을 보낸다.
- 작업자는 `dev` (또는 `frontend`, `backend`) 브랜치에서 작업 후 PR을 생성한다.

<br>

## 3.2 작업자(dev 브랜치) — PR 생성 절차

### ① 현재 브랜치 확인 및 전환
```bash
# 현재 브랜치가 dev가 아닌 경우, dev로 전환
git branch -M dev
```

> ⚠️ 작업한 내용이 `main`과 동일한 경우 비교 대상이 없으므로,  
> 아래 순서대로 push 후 GitHub에서 PR을 생성한다.

### ② 변경 사항 커밋 & 푸시
```bash
git add .
git commit -m "커밋 메시지"
git push -u origin dev
```

### ③ GitHub에서 PR 생성
1. 저장소 페이지에서 **branch 링크** 클릭
2. 브랜치 목록에서 `dev` 브랜치의 오른쪽 확장 메뉴 **[...]** 클릭
3. **[New pull request]** 선택
4. PR 제목과 설명 메시지 입력
5. **[Create pull request]** 클릭

> `base` 브랜치: `main` (병합될 대상)  
> `compare` 브랜치: `dev` (내가 작업한 브랜치)

<br>

## 3.3 팀 리더(main 관리자) — 코드 리뷰 및 결정

PR을 받은 팀 리더는 **Files changed** 탭에서 변경 사항을 확인하고, 아래 세 가지 중 하나로 결론을 내린다.

| 결정 | 의미 | 후속 조치 |
|------|------|-----------|
| **Approve** (승인) | 코드에 문제 없음 | 바로 merge 가능 |
| **Request Changes** (수정 요청) | 반드시 수정이 필요함 | 수정 후 다시 리뷰 필요 |
| **Comment** (참고 의견) | 선택적으로 반영 가능한 의견 | 작업자가 판단하여 반영 |

<br>

## 3.4 작업자 — 수정 요청(Request Changes) 대응 절차

```bash
# 1. 코드 수정 후 동일 브랜치에서 커밋 & 푸시
git add .
git commit -m "리뷰 반영: 수정 내용 설명"
git push -u origin dev
# → 기존 PR에 자동으로 커밋이 추가되며, 리뷰어에게 알림이 간다.
```

<br>

## 3.5 dev 브랜치 — main 변경 사항 동기화 (pull 먼저!)

> 코드가 맞지 않거나 충돌(conflict)이 예상되는 경우,  
> **작업 전 반드시 main을 pull한 후 작업**하도록 요청한다.

```bash
# main의 최신 내용을 dev로 가져오기
git branch -M main
git pull 레포지터리주소

# 변경 사항 비교
git diff                  # 코드 내용 비교
ls -al                    # 파일 목록 비교
# (VS Code에서 파일 내용 비교 가능)

# 필요한 작업 완료 후 다시 dev로 전환하여 push
git branch -M dev
git add .
git commit -m "커밋 메시지"
git push -u origin dev
```

<br>

## 3.6 전체 코드 리뷰 흐름 요약

```
작업자 (dev 브랜치)
  │
  ├─ git add . / commit / push
  │
  ▼
GitHub — PR 생성 (dev → main)
  │
  ▼
리뷰어 (팀 리더)
  │
  ├─ Approve     → Merge 완료 ✅
  ├─ Request Changes → 작업자 수정 후 재 push → 재리뷰
  └─ Comment     → 작업자 선택적 반영
```

<br><br>

# 4. 긴급 대처 — Rollback 실습

> Git에서 실수했을 때 상황별로 되돌리는 방법 정리  
> `rollback`은 Git 명령어가 아니라 **"개념"**이다.

<br>

## 4.1 git status (현재 상태 보기)
```bash
git status
```

- 수정된 파일 목록 확인
- staging 여부 확인

```bash
echo "v2" >> file.txt
git status
# → modified: file.txt
```

<br>

## 4.2 git log (이력 보기)
```bash
git log --oneline
```

커밋 히스토리를 한 줄씩 간결하게 확인

```bash
git commit -am "v2 commit"
git log --oneline
# → v2 commit
# → v1 commit
```

<br>

## 4.3 git checkout (과거 상태 보기)
```bash
# 과거로 이동 (읽기 전용 상태)
git checkout HEAD~1

# 원래로 돌아오기
git checkout main
```

> ⚠️ **주의**: 이 상태에서 수정하면 위험 (Detached HEAD 상태)

<br>

## 4.4 git restore (파일 되돌리기)

아직 commit 하지 않은 변경 취소

```bash
echo "v3" >> file.txt
git status        # 변경 발생 확인

git restore file.txt
# → 변경 취소됨
```

<br>

## 4.5 git reset (강력한 되돌리기)

커밋 자체를 삭제

```bash
echo "v3" >> file.txt
git commit -am "v3 commit"
git log --oneline

git reset --hard HEAD~1
# → v3 commit 완전히 삭제됨
```

> ⚠️ **주의**: 히스토리 자체가 삭제되므로 협업 환경에서 사용 금지

<br>

## 4.6 git revert (안전한 되돌리기)

기존 커밋은 유지하고 "되돌리는 새 커밋" 생성

```bash
echo "v3" >> file.txt
git commit -am "v3 commit"

git revert HEAD
# → revert 커밋 새로 생성됨
```

<br>

## 4.7 reset vs revert 비교

| 항목 | reset | revert |
|------|-------|--------|
| 히스토리 | 삭제 | 유지 |
| 안전성 | 위험 | 안전 |
| 협업 | X | O |

<br>

## 4.8 상황별 rollback 방법

| 상황 | 명령어 |
|------|--------|
| 수정 취소 (commit 전) | `git restore` |
| 커밋 삭제 | `git reset` |
| 커밋 유지하며 취소 | `git revert` |
| 과거 버전 확인 | `git checkout` |

<br>

## 4.9 실무 핵심 규칙

- **reset**은 혼자 작업할 때만 → 협업 브랜치에서 사용 시 팀원 히스토리 꼬임
- **revert**는 협업용 → push된 커밋을 되돌릴 때 항상 revert 사용
- **restore**는 습관처럼 → commit 전 실수한 코드 빠르게 되돌릴 때
