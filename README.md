# 1. git/github dev test
로컬 저장소

<br>

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
2. [remote "origin"] 항목의 	url 값에 토큰과 계정을 추가하여 내용 수정
   1. url = https://본인계정:토큰@github.com/깃허브레포지터리주소.git

 
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

# github
원격 저장소


