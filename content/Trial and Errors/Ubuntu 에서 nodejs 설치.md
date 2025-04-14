
버전 관리를 위해 macOS 에선 asdf 를 썼으나 wsl-ubuntu 환경에서 java 플러그인 제외하면 제대로 동작하지 않음.

시작하기 앞서 아래 git config 이 false 로 되어있는지 체크해야 좋다. (모두 git 을 통한 설치인데 WSL 라서)

```
git config --global core.autocrlf false
```

# python (pyenv)

asdf 도 내부적으론 pyenv 를 사용한다. 본격적으로 설치하기 전에 필요한 라이브러리들을 먼저 설치해준다.

```
sudo apt-get install libbz2-dev libncurses5-dev libffi-dev libreadline-dev libsqlite3-dev liblzma-dev
```

그 후 아래 커맨드로 설치한다.

```
curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer | bash

# .zshrc에 붙여넣기.
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --zsh)"
```

그리고 아래처럼 파이썬 버전을 관리한다.

```
pyenv install 3.9
pyenv versions
pyenv local 
```


# nodejs (nvm)

nvm 은 노드 버전 매니저임. 아래 커맨드로 설치한다.

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

2025년 1월 기준 최신 버전임.

설치 되고 나서 아래 명령어들 사용해 버전관리하면 됨.

```
nvm ls
nvm install 16.20.2
nvm run node --version
nvm use 16.20.2 (일시적으로 사용할 버전)
nvm alias default 16.20.2 (기본 버전 지정)
```


