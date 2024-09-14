
- `git add .` 보단 `git add --patch` (`GiA`) 가 더 좋다.
- 머지 커밋만 부모가 둘 이다. conflict 는 여기서 발생한다.
- `git merge --no-ff` 를 써야 명시적인 머지 커밋을 만들어준다.
- 