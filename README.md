# micss
https://polandballhub-operator.github.io/micss/
<br>ホームページも見てみよう
<br>**micss** は、フレームワークやビルドツールを必要としない、軽量な Web Components UI ライブラリです。HTML に JavaScript を1つ読み込むだけで、カード、ボタン、入力欄、トグル、スライダー、ナビゲーション、トースト、ダイアログなどを利用できます。

有名なMIなスマートフォンユーザーインターフェースに触発された、使いやすいWeb Components

## 特徴

- Vanilla JavaScript だけで動作
- Custom Elements と Shadow DOM を使用
- 外部 CSS、フレームワーク、ビルド環境が不要
- HTML の属性で基本設定が可能
- `CustomEvent` によるアプリ側との連携
- PTZ テーマ値を JavaScript から適用可能
- モダンブラウザで利用可能

## クイックスタート

### CDN から読み込む

運用環境では、jsdelivrを使用することを推奨します。

```html
<script src="https://cdn.jsdelivr.net/gh/PolandBallHub-Operator/micss@main/micsscdn.js"></script>
```

開発中に最新版を確認する場合は、次の URL も利用できます。

```html
<script src="https://cdn.jsdelivr.net/gh/PolandBallHub-Operator/micss@main/micsscdn.js"></script>
```

### 最小サンプル

```html
<!doctype html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Micss sample</title>
  <script src="https://cdn.jsdelivr.net/gh/PolandBallHub-Operator/micss@main/micsscdn.js"></script>
</head>
<body>
  <dc-card>
    <h2>Hello Micss</h2>
    <p>標準 HTML に Micss のコンポーネントを配置できます。</p>
    <dc-button id="hello-button">Action</dc-button>
  </dc-card>

  <script>
    document.querySelector('#hello-button').addEventListener('dc-press', () => {
      console.log('ボタンが押されました');
    });
  </script>
</body>
</html>
```

## コンポーネント一覧

| 要素 | 用途 | 主な属性 |
|---|---|---|
| `dc-header` | ページヘッダー | `slot="logo"` |
| `dc-theme-toggle` | ライト・ダーク切り替えボタン | `label` |
| `dc-card` | カードコンテナ | `accent`、`card-radius` など |
| `dc-list` | リストコンテナ | `accent` など |
| `dc-list-item` | リスト項目 | `slot="title"`、`slot="description"`、`slot="action"` |
| `dc-button` | ボタン | `variant`、`type`、`disabled` |
| `dc-toggle` | トグルスイッチ | `checked`、`disabled`、`name` |
| `dc-slider` | スライダー | `min`、`max`、`step`、`value`、`unit`、`label` |
| `dc-input` | 入力欄 | `type`、`value`、`placeholder`、`name`、`disabled` |
| `dc-badge` | バッジ | なし |
| `dc-color-swatch` | 色選択用スウォッチ | `color`、`active` |
| `dc-color-grid` | 色スウォッチのグループ | なし |
| `dc-nav` | 下部ナビゲーション | なし |
| `dc-nav-item` | ナビゲーション項目 | `active`、`view`、`icon`、`label` |
| `dc-view` | 表示切り替え用ビュー | `active` |
| `dc-code` | コード表示 | なし |
| `dc-toast` | 一時通知 | `open`、`message` |
| `dc-dialog` | ダイアログ | `open` |
| `dc-dropzone` | JSON ファイルドロップ領域 | なし |
| `dc-json-editor` | JSON 編集欄 | `value` |
| `dc-preset-grid` | PTZ プリセット一覧 | なし |
| `dc-ptz-provider` | PTZ 値の適用範囲 | なし |
| `dc-scroll` | スクロール領域 | なし |

## 基本コンポーネント

### ヘッダー

```html
<dc-header>
  <span slot="logo">Micss</span>
</dc-header>
```

`dc-header` は内部に `dc-theme-toggle` を配置します。テーマ切り替えボタンを表示したくない場合は、独自のヘッダーを使用してください。

### カード

```html
<dc-card>
  <h2>カードタイトル</h2>
  <p>カード本文です。</p>
</dc-card>
```

### ボタン

```html
<dc-button id="primary-button">実行</dc-button>
<dc-button variant="secondary">キャンセル</dc-button>
<dc-button disabled>無効化</dc-button>
```

ボタンが押されると、ホスト要素から `dc-press` イベントが発生します。

```js
document.querySelector('#primary-button').addEventListener('dc-press', (event) => {
  console.log('pressed', event.detail.originalEvent);
});
```

### トグル

```html
<dc-toggle id="notifications" checked></dc-toggle>
```

状態が変わると `dc-change` が発生します。

```js
document.querySelector('#notifications').addEventListener('dc-change', (event) => {
  console.log(event.detail.checked);
});
```

`event.detail.checked` は Boolean 値です。

### 入力欄

```html
<dc-input
  id="username"
  placeholder="名前を入力"
></dc-input>
```

入力中は `dc-input` が発生します。

```js
document.querySelector('#username').addEventListener('dc-input', (event) => {
  console.log(event.detail.value);
});
```

### スライダー

```html
<dc-slider
  id="progress"
  label="進捗"
  min="0"
  max="100"
  value="60"
  unit="%">
</dc-slider>
```

値が変わると `dc-input` が発生します。

```js
document.querySelector('#progress').addEventListener('dc-input', (event) => {
  console.log(event.detail.value);
});
```

`event.detail.value` は数値です。

### リスト

```html
<dc-list>
  <dc-list-item>
    <span slot="title">アクション</span>
    <span slot="description">説明文</span>
    <dc-button slot="action">実行</dc-button>
  </dc-list-item>
</dc-list>
```

## ダイアログとトースト

### ダイアログ

```html
<dc-button id="open-dialog">開く</dc-button>

<dc-dialog id="dialog">
  <h2>確認</h2>
  <p>ダイアログの内容です。</p>
  <dc-button id="close-dialog">閉じる</dc-button>
</dc-dialog>
```

```js
const dialog = document.querySelector('#dialog');

document.querySelector('#open-dialog').addEventListener('dc-press', () => {
  dialog.open();
});

document.querySelector('#close-dialog').addEventListener('dc-press', () => {
  dialog.close();
});
```

`open()` と `close()` は `open` 属性を追加・削除します。背景部分をクリックして閉じることもできます。

### トースト

```html
<dc-toast id="toast"></dc-toast>
```

```js
document.querySelector('#toast').show('保存しました');
```

`show(message, duration)` の `duration` の既定値は 2200 ミリ秒です。

## ナビゲーション

```html
<dc-nav>
  <dc-nav-item active view="overview" icon="◉" label="概要"></dc-nav-item>
  <dc-nav-item view="components" icon="▦" label="部品"></dc-nav-item>
  <dc-nav-item view="settings" icon="⚙" label="設定"></dc-nav-item>
</dc-nav>
```

項目をクリックすると `dc-nav` から `dc-navigate` が発生します。

```js
document.querySelector('dc-nav').addEventListener('dc-navigate', (event) => {
  console.log(event.detail.view);
});
```

クリックされた項目には `active` 属性が付き、以前の項目からは削除されます。

## PTZ テーマ

PTZ は、コンポーネントの見た目をページ側から調整するための設定オブジェクトです。

```html
<script type="application/json" id="micss-ptz">
{
  "themeName": "My Theme",
  "accentColor": "#3381FF",
  "cardRadius": 20,
  "sliderHeight": 20,
  "toggleWidth": 54,
  "toggleHeight": 30,
  "toggleKnobRadius": 50,
  "toggleKnobWidth": 22,
  "bgLight": "#F7F7F7",
  "bgDark": "#121212"
}
</script>

<script>
  const ptz = JSON.parse(document.querySelector('#micss-ptz').textContent);
  DesignCatalog.applyPtz(ptz);
</script>
```

JavaScript から直接適用することもできます。

```js
DesignCatalog.applyPtz({
  accentColor: '#8B5CF6',
  cardRadius: 12,
  sliderHeight: 16,
  toggleWidth: 50,
  toggleHeight: 26,
  toggleKnobWidth: 18
});
```

利用可能な公開 API は次のとおりです。

```js
DesignCatalog.PTZ_DEFAULTS
DesignCatalog.PTZ_PRESETS
DesignCatalog.applyPtz(ptz)
DesignCatalog.adjustColorBrightness(hex, percent)
```

## イベント仕様

| イベント | 発生元 | `event.detail` |
|---|---|---|
| `dc-press` | `dc-button` | `{ originalEvent }` |
| `dc-change` | `dc-toggle` | `{ checked }` |
| `dc-input` | `dc-input` | `{ value }` |
| `dc-input` | `dc-slider` | `{ value }` |
| `dc-navigate` | `dc-nav`、`dc-nav-item` | `{ view }` |
| `dc-theme-change` | `dc-theme-toggle` | `{ dark }` |
| `dc-color-change` | `dc-color-swatch`、`dc-color-grid` | `{ color }` |
| `dc-file` | `dc-dropzone` | `{ file, text }` |
| `dc-json` | `dc-json-editor` | `{ value, text }` |
| `dc-json-error` | `dc-json-editor` | `{ error }` |
| `dc-preset` | `dc-preset-grid` | `{ preset }` |
| `dc-ptz-change` | `dc-ptz-provider` | `{ ptz }` |

イベントは `bubbles: true` と `composed: true` で発生します。そのため、Shadow DOM の内部からホスト要素や通常のページ側へ伝播します。

## 修正版で変更された点

### 1. Shadow DOM の子要素順を修正

元の実装では、Shadow Root に `<style>` を先に追加していました。

```js
root.append(style(), body);
```

各コンポーネントは `root.firstElementChild` を UI 本体として扱っていたため、`<style>` が誤って書き換えられていました。fixed 版では UI 本体を先に追加します。

```js
root.append(body, style());
```

### 2. Shadow Root 全体の置換を修正

`DCJsonEditor`、`DCPTZProvider`、`DCScroll` は Shadow Root 全体を `innerHTML` で置換していました。fixed 版では UI 用の内部要素だけを更新します。

### 3. カスタム要素の表示形式を追加

カスタム要素は既定では inline 要素として扱われます。fixed 版では、カードやスクロール領域を block、ボタンやバッジを inline-block、ナビゲーション項目を flex 項目として定義しています。

### 4. テーマアイコンの外部フォント依存を削除

`light_mode` と `dark_mode` の文字列は Material Symbols が読み込まれていない環境ではそのまま表示されます。fixed 版では、外部フォントを必要としない `☼` と `☾` を使用しています。

## ブラウザ対応

Micss は Custom Elements、Shadow DOM、`CustomEvent`、`Element.closest()` などの標準 Web API を使用します。対象ブラウザでは、最新版の Chromium 系、Firefox、Safari を推奨します。古いブラウザを対象にする場合は、必要な Web Components polyfill をアプリ側で検討してください。

## セキュリティ上の注意

コンポーネントの一部では、スロットの内容や属性値を `innerHTML` に組み込んでいます。信頼できないユーザー入力を `dc-button` の内容、`dc-badge` の内容、`dc-header` のロゴ、`icon`、`label`、その他の属性値へ直接渡さないでください。外部入力を表示する場合は、アプリ側でサニタイズまたはテキストノードとしての挿入を行ってください。

CDN を利用する場合は、可変ブランチではなくコミット SHA またはリリースタグへ固定することを推奨します。必要に応じて、アプリ側で Subresource Integrity と適切な CSP も設定してください。

## 既知の注意点

`DesignCatalog.applyPtz()` の現行実装では、PTZ オブジェクトに含まれる `toggleKnobRadius`、`bgLight`、`bgDark` の一部が CSS カスタムプロパティへ完全には反映されません。これらの値を本格的にテーマへ反映する場合は、追加の実装が必要です。

また、テーマ切り替えボタンは `dark-mode` クラスを切り替えますが、アプリ側でダークテーマ用の CSS 変数を定義する必要があります。アプリ独自のダークテーマを使用する場合は、次のような CSS をページ側に追加してください。

```css
:root.dark-mode {
  --bg-base: #121212;
  --glass-bg: #1c1c1e;
  --text-main: #ffffff;
  --text-sub: #b8b8b8;
  --bg-secondary: #2c2c2e;
  --nav-bg: #1c1c1e;
  --nav-icon-active: #ffffff;
}
```
