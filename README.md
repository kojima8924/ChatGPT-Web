# ChatGPT-Web

ブラウザで動作するテキスト補完デモ。入力中にOpenAI APIを使ってリアルタイムにゴーストテキスト（補完候補）を表示します。

![JavaScript](https://img.shields.io/badge/JavaScript-Vanilla-yellow)
![HTML](https://img.shields.io/badge/Single_File-HTML-orange)
![License](https://img.shields.io/badge/License-MIT-yellow)

## 特徴

- **ゴーストテキスト補完** - 入力中にグレーの補完候補をリアルタイム表示
- **Tab / 右矢印で確定** - Tab で全体を確定、右矢印で1文字ずつ確定
- **モデル切り替え** - gpt-4o-mini / gpt-4.1-mini / gpt-5-mini / gpt-5.2 をタブで選択。カスタムモデルにも対応
- **設定パネル** - デバウンス時間、Temperature、最大トークン数、コンテキスト文字数、システムプロンプトを調整可能
- **APIキー永続化** - ブラウザの localStorage に保存
- **ステータスインジケーター** - API通信状態を緑/赤/青のドットで表示
- **ダークテーマ** - グラスモーフィズムを取り入れたダークUI
- **ビルド不要** - HTMLファイル1つで完結。サーバー不要でブラウザで直接開くだけ

## スクリーンショット

<!-- スクリーンショットを追加する場合: -->
<!-- ![デモ](docs/screenshot.png) -->

## 使い方

### 1. ファイルを開く

```bash
# ブラウザで直接開く
start index.html
```

または任意のHTTPサーバーで配信:

```bash
python -m http.server 8000
# http://localhost:8000 にアクセス
```

### 2. APIキーを設定

1. 画面上部の「API Key」欄にOpenAI APIキーを入力
2. 「Save」をクリック（localStorage に保存されます）

### 3. テキストを入力

テキストエリアに文字を入力すると、一定時間（デフォルト700ms）後にゴーストテキストが表示されます。

### キー操作

| キー | 動作 |
|---|---|
| `Tab` | ゴーストテキスト全体を確定 |
| `→` (右矢印) | 1文字ずつ確定 |
| `←` (左矢印) | 1文字取り消し |
| `Enter` / `Escape` | ゴーストテキストを破棄 |

## 設定項目

| 項目 | 範囲 | デフォルト | 説明 |
|---|---|---|---|
| Debounce | 100-2000ms | 700ms | 入力後に補完リクエストを送るまでの待機時間 |
| Temperature | 0-2 | 0.3 | 応答のランダム性 |
| Max Output Tokens | 16-512 | 80 | 補完テキストの最大長 |
| Max Context Chars | 500-10000 | 3000 | APIに送信するコンテキストの最大文字数 |
| System Prompt | - | (補完指示) | 補完の振る舞いを制御するプロンプト |

## 技術的な仕組み

- **ミラーレイヤー方式**: 透明な `textarea` の背面に `<pre>` 要素を重ねて描画。入力テキストは白、ゴーストテキストはグレーで表示
- **デバウンス**: 入力が止まってから一定時間後にAPIリクエストを送信。連続入力中のリクエスト乱発を防止
- **AbortController**: 新しいリクエスト送信時に前のリクエストをキャンセル
- **補完正規化**: APIが入力テキストを繰り返す場合に重複部分を自動除去

## 必要環境

- モダンブラウザ (Chrome / Edge / Firefox / Safari)
- OpenAI APIキー

## ファイル構成

```
ChatGPT-Web/
└── index.html    # アプリケーション全体（HTML + CSS + JavaScript）
```

## ライセンス

[MIT License](LICENSE)
