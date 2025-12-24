# krz-core - コア基盤システム

Krz-Tech Minecraft Server の基盤システムです。

## 機能

- グローバル設定管理
- **変数初期化システム（プレイヤー・サーバー設定）**
- **UXエフェクトシステム（ブートシーケンス、サウンド、Join/Quit）**
- **デバッグモード機能**
- 共通ユーティリティ関数
- メッセージ管理システム
- PlaceholderAPI統合（準備中）
- データベース接続（準備中）

## コマンド

### `/krz-config-reload`
**権限**: `krz.admin`  
**説明**: コア設定をリロードします。

```
/krz-config-reload
```

### `/krz-debug <on|off>`
**権限**: `krz.admin`  
**説明**: デバッグモードを切り替えます。

```
/krz-debug on   # デバッグモードを有効化
/krz-debug off  # デバッグモードを無効化
```

### `/krz-init-player <player>`
**権限**: `krz.admin`  
**説明**: プレイヤーの変数を強制的に再初期化します。  
**注意**: デバッグモードが有効な場合のみ使用可能です。

```
/krz-init-player <player名>
```

## 関数

### `core_log(msg: text)`
コンソールにログを出力します。

```skript
core_log("サーバー起動完了")
```

### `core_format_money(amount: number) :: text`
通貨を整形して文字列として返します。

```skript
set {_formatted} to core_format_money(1000)
# 結果: "1000c"
```

### `core_broadcast(msg: text)`
全プレイヤーにメッセージをブロードキャストします。

```skript
core_broadcast("サーバーメンテナンスを開始します")
```

### `core_msg(p: player, key: text)`
定義済みメッセージをプレイヤーに送信します。

```skript
core_msg(player, "no_permission")
```

### `init_player_vars(p: player)`
プレイヤーの全変数を初期値で設定します。

```skript
init_player_vars(player)
```

### `init_server_config()`
サーバー設定変数を初期化します（VariableReference.md準拠）。

```skript
init_server_config()
```

### `core_debug_log(msg: text)`
デバッグモードが有効な場合のみログを出力します。

```skript
core_debug_log("変数初期化完了")
```

### `fx_boot_sequence(p: player)`
ログイン時のブートシーケンスアニメーションを実行します。
盲目エフェクト、Titleアニメーション、パーティクル、サウンド、ActionBarを含みます。

```skript
fx_boot_sequence(player)
```

### `sfx_login(p: player)`
ログイン時のコンポジットサウンドを再生します。

```skript
sfx_login(player)
```

### `sfx_success(p: player)` / `sfx_error(p: player)`
成功/エラー時のサウンドフィードバックを再生します。

```skript
sfx_success(player)
sfx_error(player)
```

### `sfx_gui_open(p: player)` / `sfx_gui_close(p: player)` / `sfx_click(p: player)`
GUI操作時のサウンドフィードバックを再生します。

```skript
sfx_gui_open(player)
sfx_gui_close(player)
sfx_click(player)
```

## 設定変数

| 変数 | デフォルト値 | 説明 |
|-----|------------|------|
| `{-krz::config::prefix}` | `&b[Tech] &r` | サーバープレフィックス |
| `{-krz::config::version}` | `1.0.0` | バージョン |
| `{-krz::config::debug_mode}` | `false` | デバッグモード |
| `{-krz::config::db_host}` | `db-service` | DB接続先 |

## メッセージ

| キー | メッセージ |
|-----|-----------|
| `no_permission` | 権限がありません。 |
| `error_general` | エラーが発生しました。 |
| `success_general` | 処理が成功しました。 |
