# AGENTS.md

このリポジトリは Misskey upstream tag `2026.3.2` をベースにした fork です。
merge-base は `b97683cdb2315daf6f01c423809c872fd4be7948`、作成時点の HEAD は `6e61072de3` です。

## original Misskey との差分メモ

- バージョンと repository は `2026.3.2-nicomedkey` / `uboar/nicomedkey` に変更されています。
- Docker publish workflow は `nicomedkey/nicomedkey` への publish と、`main` push / package version tagging に合わせています。
- `misskeyBlockMentionsFromUnfamiliarRemoteUsers` 設定で、未知の remote user からの通知発生投稿を抑止できます。
- visitor / nav / splash / widget UI には nicomedkey logo、branding、fork GitHub URL が入っています。
- `imageUrl === niconico` の広告 iframe 表示と、admin 側の URL / 動画 ID ラベルに対応しています。
- kakenuke sound preset と mp3 asset が追加されています。
- upstream release 追従用に、local の `update-nicomedkey` / source-command workflow があります。

このファイル以外の既存編集は他作業者のものとして扱い、明示依頼なしに revert しないでください。
