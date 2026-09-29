# NAVI AI Chat

ChatGPT と Gemini を切り替えて使う、GitHub Pages + Railway Gateway 構成のPWAチャットです。

## 構成

- Frontend: GitHub Pages `Koran-xyz/Chatbot_AI`
- Gateway: Railway `navi-api-production-42c9.up.railway.app`
- AI: OpenAI / Gemini
- 外部自由領域: Gateway側で参照

## セキュリティ方針

OpenAI / Gemini のAPIキーはGitHub PagesやブラウザのlocalStorageへ保存しません。
APIキーはRailway側の環境変数だけで管理します。

ブラウザに入力するのは `GATEWAY_CHAT_KEY` のみで、`sessionStorage` に保存するためブラウザを閉じると消えます。

保護されたメタルール本文はサーバー内部でのみAIへ渡し、ブラウザ/APIレスポンスには返しません。

## Railwayで必要な環境変数

- `GATEWAY_CHAT_KEY`
- `ALLOWED_ORIGIN=https://koran-xyz.github.io`
- `OPENAI_API_KEY`
- `OPENAI_MODEL`（例: `gpt-5.6-luna`）
- `GEMINI_API_KEY`
- `GEMINI_MODEL`（例: `gemini-3.6-flash`）
- `NAVI_META_RULES`（利用する場合のみ。公開リポジトリには書かない）

## GitHub Pages

Settings → Pages → Deploy from a branch → `main` / `/(root)`

公開URL:
`https://koran-xyz.github.io/Chatbot_AI/`

## PWA

`index.html`, `manifest.json`, `sw.js`, `icon.svg` で構成しています。
Service Worker はGitHub Pages上の静的ファイルだけをキャッシュし、GatewayやAI API通信はキャッシュしません。
