## 명령어 재활용

함수 이용

`~/.zshrc`:

```bash
marktext() {
    open -a /Applications/Mark\ Text.app $1
}
```

alias 이용

`~/.zshrc`:

```bash
alias marktext = "open -a /Applications/Mark\ Text.app"
```
