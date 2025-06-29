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

## config備忘録

roBa.keymapの設定について

### macro

https://zmk.dev/docs/keymaps/behaviors/macros

`to_layer_0: to_layer_0`

デフォルトレイヤーに戻すマクロの定義。後述の`lt_to_layer_0`と組み合わせて使われている。

```
compatible = "zmk,behavior-macro-one-param";
#binding-cells = <1>;
bindings = <&to 0 &macro_param_1to1 &kp MACRO_PLACEHOLDER>;
```

パラメーターを1つとることを宣言しており、レイヤーを0に移動しつつ、指定されたパラメーターのキーを押すという動作になっている。

ちなみに`&to`はTO LAYER
https://zmk.dev/docs/keymaps/behaviors/layers

macrosを使うことで複数のキーコードを一つのキーに割り当てるといったこともできる。
（例えば寿限無のフルネームを1つのキーに割り当てるとか）

### behavior

https://zmk.dev/docs/config/behaviors

`lt_to_layer_0: lt_to_layer_0`

この設定ではHold and Tapの動作をカスタマイズする設定。
Hold時には&mo(レイヤーを押している間だけ有効化する)、タップ時にはデフォルトレイヤーに戻しつつ指定のキーを押すという動作になる。
