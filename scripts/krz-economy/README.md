# krz-economy - エコノミーシステム

プレイヤーの通貨管理と取引システムです。

## 機能

- プレイヤー残高管理
- 管理者向け残高操作コマンド
- 取引ログ記録
- ショップシステム（開発中）

## プレイヤーコマンド

### `/balance [プレイヤー]`
**エイリアス**: `/bal`, `/money`  
**説明**: 自分または他プレイヤーの残高を表示します。

```
/balance
/balance kurazuuuuuu
```

**出力例**:
```
[Economy] 残高: 1000c
```

### `/shop`
**説明**: ショップを開きます（開発中）。

```
/shop
```

## 管理者コマンド

### `/eco <set|add|remove> <プレイヤー> <金額>`
**権限**: `krz.admin`  
**説明**: プレイヤーの残高を操作します。

```
/eco set kurazuuuuuu 5000   # 残高を5000cに設定
/eco add kurazuuuuuu 1000   # 1000c追加
/eco remove kurazuuuuuu 500 # 500c削除
```

## 関数

### `econ_get_balance(p: player) :: number`
プレイヤーの残高を取得します。

```skript
set {_balance} to econ_get_balance(player)
```

### `econ_add(p: player, amount: number)`
プレイヤーの残高に金額を追加します。

```skript
econ_add(player, 100)
```

### `econ_remove(p: player, amount: number) :: boolean`
プレイヤーの残高から金額を削除します。残高不足の場合はfalseを返します。

```skript
if econ_remove(player, 100) is true:
    send "100c支払いました" to player
else:
    send "残高不足です" to player
```

### `econ_set(p: player, amount: number)`
プレイヤーの残高を設定します。

```skript
econ_set(player, 1000)
```

### `econ_has(p: player, amount: number) :: boolean`
プレイヤーが指定金額を持っているか確認します。

```skript
if econ_has(player, 500) is true:
    send "500c以上持っています" to player
```

## 初期設定

| 設定 | 値 |
|-----|-----|
| 初期残高 | 1000c |
| 通貨記号 | c |

## データ保存

プレイヤーの残高は `{-kp::%player's uuid%::balance}` に保存されます。
