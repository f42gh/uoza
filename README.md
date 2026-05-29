# uoza_karabiner.json

このディレクトリには、Karabiner-Elements 用の個人設定 `uoza_karabiner.json` があります。  
主に独自配列のキー入れ替えと、いくつかの補助ルールを定義しています。

## ファイル概要

- ファイル名: `uoza_karabiner.json`
- 用途: Karabiner-Elements の `karabiner.json` として使う設定ファイル
- プロファイル数: 3
  - `pisces0.1`
  - `Pisces0.2`（現在選択中）
  - `Default`

## グローバル設定

- メニューバーアイコンは非表示: `show_in_menu_bar: false`
- プロファイル名は表示: `show_profile_name_in_menu_bar: true`

## プロファイル説明

### `pisces0.1`

初期版の配列設定です。

- `virtual_hid_keyboard.keyboard_type_v2`: `iso`
- `devices` 配下で「キーボードであるデバイス」にだけ `simple_modifications` を適用
- `caps_lock` に対する `complex_modifications` あり
- `fn_function_keys` で `F3 -> caps_lock`

#### 主なキー置換

| 元のキー | 変換先 |
| --- | --- |
| `b` | `-` |
| `caps_lock` | `fn` |
| `,` | `f` |
| `f` | `t` |
| `` ` `` | `non_us_backslash` |
| `-` | `;` |
| `j` | `n` |
| `n` | `b` |
| `.` | `q` |
| `q` | `j` |
| `;` | `w` |
| `t` | `,` |
| `u` | `y` |
| `w` | `u` |
| `y` | `.` |

#### 複雑なルール

- `caps_lock` を `command + shift + caps_lock` に変換
  - JSON 上の description は `Change caps_lock to command+shift+caps_lock：.` となっています
  - 実際には `left_command`, `left_shift`, `caps_lock` を伴う送出になっています

### `Pisces0.2`

`pisces0.1` の発展版で、現在有効なプロファイルです。

- `selected: true`
- `virtual_hid_keyboard.keyboard_type_v2`: `ansi`
- `simple_modifications` はプロファイル直下に定義
- `fn_function_keys` で `F3 -> caps_lock`

#### 主なキー置換

`pisces0.1` とほぼ同じで、以下を含みます。

| 元のキー | 変換先 |
| --- | --- |
| `b` | `-` |
| `caps_lock` | `fn` |
| `,` | `f` |
| `f` | `t` |
| `-` | `;` |
| `j` | `n` |
| `n` | `b` |
| `.` | `q` |
| `q` | `j` |
| `;` | `w` |
| `t` | `,` |
| `u` | `y` |
| `w` | `u` |
| `y` | `.` |

`pisces0.1` にあった `` ` -> non_us_backslash `` は `Pisces0.2` にはありません。

#### 複雑なルール

1. 右 `command` 単押しで `Ctrl + M` を送る
   - 条件: 日本語入力中のみ
   - 判定条件: `input_source_if` で `language: ^ja$`
   - 単押し時: `Ctrl + M`
   - 修飾キーとして使った場合: 通常の `right_command`

2. `test`
   - `enabled: false` のため無効
   - 内容:
     - `left_shift + caps_lock` -> `page_down`
     - `right_shift + caps_lock` -> `command + mission_control`

### `Default`

最小構成の予備プロファイルです。

- 名前のみ定義
- `virtual_hid_keyboard.keyboard_type_v2`: `ansi`

## 使い方

Karabiner-Elements のメイン設定として使う場合は、通常の `karabiner.json` に反映します。

一般的な場所:

```text
~/.config/karabiner/karabiner.json
```

例えばこのファイルを内容ごと反映する運用を想定しています。

## 設定のポイント

- 独自配列の中心は `simple_modifications`
- `caps_lock` は両プロファイルで `fn` に変更
- `F3` は `caps_lock` に変更
- `Pisces0.2` では、日本語入力中だけ右 `command` 単押しに別動作を割り当て
- `pisces0.1` と `Pisces0.2` では仮想キーボード種別が `iso` / `ansi` で異なる

## メモ

- `caps_lock` の description にあった末尾の不要な記号（`：.`）を修正しました
