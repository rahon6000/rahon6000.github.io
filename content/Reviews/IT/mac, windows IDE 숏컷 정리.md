vim, ideavim, vscode 단축키 정리. windows mac 다른 부분도 있음.
mac 에선 vim 을 계속 쓸 것 같은데 windows 에선 디폴트 설정 쓸 것 같음... 그냥 bilingual 할래.

mac 에선 vim 이 편함. (ctrl cmd 분리되어 쓰기 편함.) windows 에선 갠적으로 좀 불편해서 vscode 에서 vim 플러그인을 안쓰기로 했음.

# 커서 이동, 에디터

vim 처럼 방향키를 거의 안쓸 순 없다. vim 에서의 w, b, f, / 같은 네비게이션 성격의 키들을 사용할 수 없고 방향키와 기능키 조합을 써야 한다.
 
- word
    - vim : w, e, b
    - win : ctrl + arrow
- line
    - vim : $, ^, Shift commands
    - win : Home, End (Fn + arrow), Some shift commands
- line shift
    - vim : cmd + shift + arrow
    - win : alt + arrow
- paragraph
    - vim : {, }
    - win : 
- document
    - vim : gg, G
    - win : Ctrl + Home/End (Ctrl + Fn + arrow)
- search
    - vim : f, /, #, %
    - win : ctrl f
- multi cursor
    - vim : ctrl g, visual mode...
    - win : ctrl + d, alt + click, ctrl + alt + arrow
- definition
    - vim : gd
    - win : F12
- debug
    - vim : F8, F7
    - win : F9 ~ F11

# 에디터 탭 및 기타 탭 이동

- tab switch
    - vim : cmd + opt + arrow
    - win : ctrl + Page (ctrl + Fn + arrow), ctrl + p
- tab group
    - vim : 
    - win : ctrl + 1 (select), ctrl + \\ (split)
- explorer
    - vim : cmd + 1 (IdeaVim)
    - win : ctrl + E
- terminal
    - vim : cmd + F12
    - win : ctrl + `


- 서치/네비게이션

ctrl t : 심볼 조회
ctrl g : go to line (vime 의 : 에 해당)
ctrl p : go to file
ctrl O : go to symbol (지원 포맷만)
F8 : 다음 에러,경고 (intelliJ 에선 F2 였나 그럴거임)

# 명령어 관련



ctrl r : open recent
ctrl h : replace (intelliJ 처럼 ctrl r 이 아니다.)
ctrl d : 같은 단어 멀티 선택 (ideaVim 의 ctrl g 같은 느낌) 추가적인 용법으로 현재 단어 선택 (vim 의 viw) 기능처럼 쓸 수 있다.
ctrl k ctrl d : 다음 단어 찾기 (vim 에도 비슷한 거 있으면 유용할듯. *, # 으로 가능하다고 한다. 왜 안썼지..)

alt r : vscode 검색은 regex 사용이 가능하다. regex 심볼이 거슬리면 이 키로 regex 사용 토글한다. (자매품 alt c, alt w)
ctrl alt up/down : 위 아래 커서삽입. (vim 에 해당 기능있으면 좋겠다)


선택 + left parenthesis : 알아서 감싸준다. vim 에선 손쉽게 사용안된다...
ctrl L : 현재 선택된 내용 모두 선택 (ctrl F2 와 비슷한데 약간 다르다. 파일 내에서 rename 할 때 유용함.)
alt shift left/right : expand/shrink selection (inelliJ 에도 비슷한 키 있었음.)
ctrl alt shift arrow : 박스 선택 (vim 의 ctrl v 같은 느낌.)

ctrl shift space : 파라미터 힌트 보여주기 (예전엔 몰라서 메서드명 썻다 지웠다 했었다... ㅡㅡ)
F12 : 정의로 이동 (intellij 의 ctrl alt b 였나 아마 그럴거임 vim 에선 gd 로 했었음.)
F2 : 리네임 (inellij 에선 F6) 
alt shift f : 문서 리포맷 (intelliJ 에선 ctrl alt l 이었나 그럴 거임.)


얘네들은 mac 에서 같은지 체크 필요
ctrl 1 : 탭 그룹 선택
alt 1 : 탭 선택

ctrl \ : 탭 스플릿

ctrl shift up/down : 탭 위치이동 (와)

디버그 키
디버그 숏컷은 특히나 intelliJ 하고 다름 (열받아)
F9 : 브레이크 설정 (intelliJ 의 cmd F8)
F5 : 속행 (intelliJ 의 cmd alt r 이었나?)
F11 : step in (intelliJ 의 F7)
F10 : step over (intelliJ 의 F8)

포커스, 화면 관련
ctrl b : 사이드바 토글
ctrl ` : 터미널 토글 및 포커스
ctrl 1 : 에디터 (그룹1) 포커스 (다른 방법도 많다.)


검색
ctrl shift p : 명령어
ctrl shift o : 심볼
ctrl e : 파일 (프로젝트 밖이어도 열려있으면 검색. intelliJ 의 ctrl shift o)



