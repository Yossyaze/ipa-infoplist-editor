# IPA Info.plist Editor (MVP)

公開URL: https://yossyaze.github.io/ipa-infoplist-editor/

ブラウザ上で `.ipa` / `.zip` を読み込み、`Payload/*.app/Info.plist` の基本情報を編集して再保存するツールです。

## 使い方

1. `index.html` をブラウザで開く。
2. `.ipa` または `.zip` をドラッグ&ドロップ。
3. 以下の項目を編集。
   - `CFBundleDisplayName` / `CFBundleName`
   - `CFBundleIdentifier`
   - `CFBundleShortVersionString`
   - `CFBundleVersion`
   - `MinimumOSVersion`
4. 「編集したIPAを保存」を押して `_edited` 付きファイルをダウンロード。

## 現在の仕様

- `Payload/*.app/Info.plist` を検出して最初の1件を使用。
- XML plist と Binary plist を判定して読み込み。
- 保存時は XML plist として再生成。
- フォーム編集中に下部プレビューへ即時反映。
- 保存前バリデーション:
  - `CFBundleIdentifier` は必須
  - `CFBundleIdentifier` 形式チェック
  - `MinimumOSVersion` 形式チェック（例: `14`, `14.0`, `14.0.1`）

## 重要な注意

Info.plist を変更した IPA は既存の電子署名が無効になります。
実機インストールには再署名（Resign）が必要です。

## 動作確認チェックリスト

- 正常系
  - [ ] `.ipa` 読み込み成功
  - [ ] 基本項目の表示・編集成功
  - [ ] 保存後 `_edited` ファイルを取得できる
- 異常系
  - [ ] 非 `.ipa/.zip` でエラー表示
  - [ ] `Info.plist` 不在でエラー表示
  - [ ] 不正な `Bundle ID` で保存ブロック

## 配布用の最小構成

- `index.html`: アプリ本体（そのままブラウザで実行可能）
- `README.md`: 使い方と注意事項

必要に応じて、手元で任意の `.ipa` / `.zip` を用意して上記チェックリストを実施してください。
