# zmk-config-roBa

<img src="keymap-drawer/roBa.svg" >

# zmk firmware

https://zmk.dev/docs

QMKと違ってGitHub Actionsでファームウェアのビルドが行われる（ZMKの本体をインストールといった手間が不要）

boards: 物理ボード（roBaではXIAO nRF52840）

shields: キーボードのカラムレイアウトや左右分割といった設定単位

zephyr: OS

## 設定変更

https://zmk.dev/docs/config

### キーマップ

config/roBa.keymapで設定

https://zmk.dev/docs/config

### その他の設定

config/boards/shields/Test以下のファイルを設定変更

keymap-drawerは触らない（GitHub Actionsによって生成されコミットが行われる）

