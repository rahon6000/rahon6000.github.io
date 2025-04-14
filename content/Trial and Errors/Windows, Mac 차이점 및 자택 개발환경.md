Mac 에서 편하게 되던거 안되는 부분 개선해야 함.

1. IDE 단축키 이슈

   - cmd/ctrl 분리가 안되어서 vscode 의 멀티커서 단축키가 다름 (mac 에선 idea keymap 으로 ctrl + g 였다.)
   - 마찬가지로 intelliJ 에선 기본 copy paste 못씀. (vim 하고 충돌)
   -

2. CLI 불편한점 다수

   - 단어 점프랑 삭제등이 Ctrl, Alt 혼재되어 있음.
   - 한글 입력이 안됨

3. kibana 더블클릭으로 전부선택이 안됨.

   - 이건 파폭이슈일수도


---

- 문단 점프는 vscode 에서 키 바인딩을 만들어주면 가능하긴 하다.

`keybinding.json` 은 명령어 shortcut 으로 검색하면 찾을 수 있다.

```json
// Place your key bindings in this file to override the defaults
[
    {
        "key": "alt+[",    // whatever keybinding you want
        "command": "cursorMove",
        "args": {
            "to": "prevBlankLine",
            "select": false         // false is the default if omitted
        },
        "when": "editorTextFocus"
    },
    {
        "key": "alt+]",
        "command": "cursorMove",
        "args": {
            "to": "nextBlankLine",
            "select": false         // false is the default if omitted
        },
        "when": "editorTextFocus"
    },
    {
        "key": "alt+shift+[",    // whatever keybinding you want
        "command": "cursorMove",
        "args": {
            "to": "prevBlankLine",
            "select": true         
        },
        "when": "editorTextFocus"
    },
    {
        "key": "alt+shift+]",
        "command": "cursorMove",
        "args": {
            "to": "nextBlankLine",
            "select": true         
        },
        "when": "editorTextFocus"
    },
]
```

