---
title: Obsidian 퍼블리시 (Quartz)
---

옵시디언 문서가 Github 에 계속 푸시되고 있는데, 얘를 어디서나 볼 수 있게 웹으로 퍼블리시 하고 싶음.

[Quartz 공식 페이지](https://quartz.jzhao.xyz/) 보면 나름 잘 되어있는 것 같으니, 이걸로 도전해 보자.


Quartz 사용법
- windows 에선 기본적으로 WSL 사용해서 터미널 작업
- 옵시디언으로 컨텐츠 작성. (어디까지나 static page 임.)
- `npx quartz build --serve` 로 로컬 테스트
- Github Desktop 사용해서 반영
	- ssh 설정하기 귀찮아서 `npx quartz sync` 사용 안함.
	- 싱크 과정도 자동이거나 주기적으로 해줬으면 편할듯? 옵시디언 플러그인이나 윈도우 기능중에 적당한 게 있을 듯.
- [공식 문서](https://quartz.jzhao.xyz/) 참조해서 문서 작성 및 커스터마이즈
- `contents` 폴더에 `index.md` 가 없으면 rss feed 가 먼저 뜨게 되니 주의
	- rss feed 는 `host/index.xml` 기본값으로 확인 가능. 아무 설정 없으면 link 가 `https://quartz.jzhao.xyz` 를 baseurl 로 가지니, config 파일을 수정해야 한다.

Jekyell 하고 비슷한데, 옵시디언을 잘 지원하는 것 같아서 좋은 느낌임.


# Todo

- [ ] 타이틀 수정
- [ ] 랜덤 페이지 기능