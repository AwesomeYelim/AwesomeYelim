# 자꾸 잊어먹는 내 자신을 위한 여러 터미널 명령키 정리

## 만약 맥북에서 yarn 을 잃어버렸다면

- 자꾸 이런메세지가 뜬다..

```
zsh: command not found: yarn
```

- 터미널에 환경변수를 다시 설정해주어야 하는걸로 판단..

```sh
sudo npm install -g yarn
```

```
password: <개인컴터비번>
```

## git config 명령어 사용법

### 설정 범위와 설정 파일

- Git은 지역(local), 전역(global), 시스템(system) 이렇게 크게 3가지 범위로 설정이 가능

- 지역(local) : 특정 저장소(repository)로 한정, 저장소 폴더의 `.git/config` 에 저장
- 전역(global) : 현재 사용자(user)의 모든 저장소를 포함, 운영체제의 사용자 폴더의 `.gitconfig`에 저장
- 시스템(system) : 해당 컴퓨터의 모든 저장소와 사용자를 걸쳐서 적용

### 사용방법

#### 01. 설정쓰기

- 옵션을 주지 않으면 기본적으로 지역(local) 범위에서 설정이 이루짐

```sh
$ git config <이름> <값>
$ git config --<범위> <이름> <값> // 범위 설정
```

#### 02. 설정읽기

```sh
$ git config --list
$ git config <이름>
```

#### 03. 설정지우기

```sh
$ git config --unset <이름>
$ git config --global --unset <이름> // 범위 설정
```
