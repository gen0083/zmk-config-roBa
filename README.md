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

キーコード
https://zmk.dev/docs/keymaps/list-of-keycodes

### その他の設定

boards/shields/roBa以下のファイルを設定変更

keymap-drawerは触らない（GitHub Actionsによって生成されコミットが行われる）

## config備忘録

roBa.keymapの設定について

### combos

複数のキーを同時に押した際の挙動を変更する設定。

```
        tab {
            bindings = <&kp TAB>;
            key-positions = <11 12>;
        };
```

キーの11と12を同時に押すとTABを入力されたとして扱う機能。
どのキーが該当するかは/config/roBa.jsonを参照するしかないっぽい？（最初に定義されているものから0インデックで指定）

キーの数は2つである必要はなく、3つでもよいし、別に横並びで並んでいる必要もない。
デフォルトでは50ミリ秒以内に押されたキーはcombosとして扱うことになっている。

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

### config/west.yml

Zephyrの依存リポジトリを指定するファイル
ZephyrはZMKのOSに相当するもの
