
git 을 호스팅 하는 가장 유명한 사이트인 github 에선 2021 년 이후로 username & password 를 사용한 인증을 deprecate 시켜버렸지만, 여전히 많은 어플리케이션들은 username & password 를 이용해 인증하고 있다. (사실 github 만의 특수성이긴 하니까.)

private key 를 따로 보관해야 하는 불편함이 있어 환경 구축시 정말 귀찮은데, 이번 기회에 적당히 정리해두려 한다.

[관련된 github 공식 페이지](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

왜 안되나 했더니 다른 계정에서 쓰던 키만 등록되어 있었다...

여러 private repository 혹은 계정들을 이용하려면 여러 키가 있어야 하나?

ssh 에서 사용하는 키를 상황에 따라 바꿔줘야 할 것 같은데. 귀찮긴 하지만 설정이 있긴 하다.

```
Host github.com github.com
        HostName github.com
        IdentityFile ~/.ssh/id_ed25519
        User git

Host github-another github.com
        HostName github.com
        IdentityFile ~/.ssh/id_ed25519_another
        User git
```

위처럼 ~/.ssh/config 파일으 설정해두면... `ssh -T git@github.com` 으로 테스트하면 처음 셋팅으로 키를 사용하고, `ssh -T github-another` 로 테스트하면 두 번째 셋팅으로 키를 사용한다.

이제 another 키를 사용하는 git repository 의 설정을 바꿔준다.

```
git remote set-url github-another:organization/repository.git

// 원래는 https://github.com/organization/repository.git 으로 되어있는 걸 수정
```

깃허브에서 클론 주소를 따올 때도 보이지만 위 형식만 맞춰주면 된다. 따로 ssh config 의 alias 를 사용하지 않으면 기본적으론 `git@github.com:org/rep.git` 형식인데, ssh config 의 alias 를 사용해주면 자연스럽게 설정해 둔 키와 유저 (`git@`) 사용하게 된다. 

git clone 으로 따올때도, 설정해준 alias 로 교체해서 사용하면 된다.

---

사실 생각보다 복잡한 부분은 없는데 디테일한 부분에서 좀 짜증나는 편이다.

1. 키 생성 및 등록, ssh-agent. 이 부분은 github 공식 페이지에 잘 설명되어있다.
2. ssh config 설정 방법. (host 와 key 맵핑)
3. git config --local 의 설정. (ssh host alias 로 치환하는 부분)

위처럼 WSL 상에서 ssh alias 를 사용하도록 설정하면 github desktop 은 제대로 작동을 못하는데, github desktop 이 WSL 위에서 작동하는게 아니라서, 윈도우즈 기본 SSH 설정을 쓰기 떄문일 것 같다. 아마 윈도우즈 기본 SSH 설정에도 WSL 에서 정한 config 을 맞춰주면 잘 작동할 것 같다.