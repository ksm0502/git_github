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
123