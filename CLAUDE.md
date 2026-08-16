# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## プロジェクトの状態

タスクボードアプリ（タスクの追加・完了切り替え・削除、`localStorage`への永続化）。

## デプロイ先

https://naomatu2015-design.github.io/task-board/

`main` ブランチへの `push` をトリガーに `.github/workflows/deploy.yml` がビルドし、GitHub Pagesへ自動デプロイする。手動デプロイは不要。

## 技術スタック

- React 19 + Vite（`@vitejs/plugin-react`）
- Lint: oxlint（`npm run lint`）
- スタイルはプレーンCSS（CSSフレームワーク・CSS-in-JSは未導入）
- 状態管理はReactの `useState`/`useEffect` のみ（外部の状態管理ライブラリは未導入）
- データ永続化は `localStorage`（バックエンド・DBは無し）

### 主なコマンド

- `npm run dev` — 開発サーバー起動
- `npm run build` — 本番ビルド（`dist/` に出力）
- `npm run lint` — oxlintによる静的解析
- `npm run preview` — ビルド済み成果物のプレビュー

## コンポーネント命名規約

現状は `src/App.jsx` に単一コンポーネントとして実装されている。今後コンポーネントを分割する際は、既存コードのスタイルに合わせて以下に従うこと。

- コンポーネントファイルは `PascalCase.jsx`（例: `App.jsx`）。対応するスタイルは同名の `PascalCase.css`（例: `App.css`）としてコンポーネントと同じディレクトリに置く
- イベントハンドラ・関数は `動詞+名詞` のcamelCase（例: `addTask`, `toggleTask`, `deleteTask`）
- 定数は `UPPER_SNAKE_CASE`（例: `STORAGE_KEY`）
- CSSクラス名はkebab-case（例: `task-form`, `task-list`, `delete-button`）

## Git運用ルール

**コードに変更を加えるたびに、コミットしてGitHubへプッシュすること。** 変更を未プッシュのままローカルに溜め込まない。

- 意味のあるまとまりで変更ができたら、都度コミットする（コミットメッセージは変更内容が分かるように書く）
- コミット後は速やかに `git push` してリモート（GitHub）に反映する
- 作業を中断・完了する際に、ローカルにのみ存在する未プッシュの変更を残さない
- リモート未設定（このリポジトリはまだ `git init` もされていない）の場合は、先に `git init` とGitHubリポジトリへの接続（`git remote add origin <URL>`）を行ってからこのルールを適用する
- force push（`git push --force`）など破壊的な操作は、ユーザーの明示的な許可なく行わない
