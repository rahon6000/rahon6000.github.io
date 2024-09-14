---
title: Obsidian 퍼블리시 (Quartz)
---

Quartz 사용법
- windows 에선 기본적으로 WSL 사용해서 터미널 작업
- 옵시디언으로 컨텐츠 작성. (어디까지나 static page 임.)
- `npx quartz build --serve` 로 로컬 테스트
- [공식 문서](https://quartz.jzhao.xyz/) 참조해서 문서 작성 및 커스터마이즈
- `contents` 폴더에 `index.md` 가 없으면 rss feed 가 먼저 뜨게 되니 주의
	- rss feed 는 `host/index.xml` 기본값으로 확인 가능. 아무 설정 없으면 link 가 `https://quartz.jzhao.xyz` 를 baseurl 로 가지니, config 파일을 수정해야 한다.