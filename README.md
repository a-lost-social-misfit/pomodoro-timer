# 🍅 Pomodoro Timer with BGM

作業用BGM付きのポモドーロタイマーです。集中力を高めるためのシンプルなbashスクリプトで、YouTubeから自動的にBGMを再生します。

## ✨ 特徴

- ⏱️ **ポモドーロテクニック**: カスタマイズ可能な作業時間と休憩時間
- 🎵 **自動BGM再生**: YouTubeからランダムにピアノ系作業用BGMを自動再生
- 📊 **カウントダウン表示**: リアルタイムで残り時間を表示
- 🔔 **通知音**: 作業・休憩の切り替え時にベル音で通知（3回）
- 📈 **セッション数カウント**: 何セッション完了したか記録
- 🎯 **柔軟な設定**: 起動時に作業時間・休憩時間を自由に設定可能

## 📋 必要なもの

このスクリプトを実行するには以下のツールが必要です：

- **Bash**: Linux / macOS / WSL
- **yt-dlp**: YouTube動画の取得用
- **mpv**: 音声再生用

## 🔧 インストール方法

### Ubuntu / Debian

```bash
# パッケージリストを更新
sudo apt-get update

# yt-dlpとmpvをインストール
sudo apt-get install -y yt-dlp mpv
```

### macOS (Homebrew)

```bash
# Homebrewがない場合は先にインストール
# /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# yt-dlpとmpvをインストール
brew install yt-dlp mpv
```

### Arch Linux

```bash
sudo pacman -S yt-dlp mpv
```

### Fedora / RHEL / CentOS

```bash
# EPELリポジトリを有効化（RHEL/CentOSの場合）
# sudo dnf install epel-release

sudo dnf install yt-dlp mpv
```

### インストール確認

以下のコマンドでインストールが成功したか確認できます：

```bash
yt-dlp --version
mpv --version
```

両方ともバージョン情報が表示されればOKです。

## 🚀 使い方

### 1. スクリプトをダウンロード

```bash
# wgetを使う場合
wget https://raw.githubusercontent.com/a-lost-social-misfit/pomodoro-timer/main/pomodoro_timer.sh

# curlを使う場合
curl -O https://raw.githubusercontent.com/a-lost-social-misfit/pomodoro-timer/main/pomodoro_timer.sh
```

### 2. 実行権限を付与

```bash
chmod +x pomodoro_timer
```

### 3. 実行

```bash
./pomodoro_timer
```

### 4. 時間を設定

起動すると以下のように時間設定を聞かれます：

```
🍅 ポモドーロタイマー with BGM
================================

⚙️  時間設定:

作業時間を入力してください（分）[デフォルト: 25]: 30
休憩時間を入力してください（分）[デフォルト: 5]: 10

✅ 設定完了:
  作業時間: 30分
  休憩時間: 10分

この設定で開始しますか？ (y/n): y
```

- **Enterキーのみ**: デフォルト値（作業25分/休憩5分）を使用
- **数字を入力**: 好きな時間（分）を設定
- **テスト用**: `1`と`1`を入力すると1分ずつで動作確認できます

## 💡 使用例

### 標準的なポモドーロ（25分作業 / 5分休憩）

```bash
./pomodoro_timer.sh
# 作業時間: Enter（デフォルト25分）
# 休憩時間: Enter（デフォルト5分）
```

### カスタム設定（50分作業 / 10分休憩）

```bash
./pomodoro_timer.sh
# 作業時間: 50
# 休憩時間: 10
```

### テスト実行（1分作業 / 1分休憩）

```bash
./pomodoro_timer.sh
# 作業時間: 1
# 休憩時間: 1
```

## 🎵 BGMについて

以下のキーワードでYouTubeを検索し、ランダムに1つを選んで自動再生します：

- piano study music 1 hour
- relaxing piano focus music
- lofi piano study beats
- calm piano concentration music
- ambient piano work music

BGMの音量は50%に設定されています。変更したい場合はスクリプト内の`--volume=50`の数値を編集してください。

## ⌨️ 操作方法

- **y + Enter**: 次に進む（休憩開始/次のセッション開始）
- **n + Enter**: タイマーを終了
- **Ctrl + C**: 即座に終了（BGMも自動停止）

## 🐛 トラブルシューティング

### エラー: コマンドがインストールされていません

```
❌ 以下のコマンドがインストールされていません: yt-dlp mpv
```

**解決方法**: 上記の「インストール方法」に従って`yt-dlp`と`mpv`をインストールしてください。

### BGMが再生されない

**原因と解決方法**:

1. **インターネット接続を確認**
   ```bash
   ping -c 3 youtube.com
   ```

2. **yt-dlpが正しく動作するか確認**
   ```bash
   yt-dlp --get-id "ytsearch1:piano study music"
   ```

3. **mpvが正しく動作するか確認**
   ```bash
   mpv --no-video "https://www.youtube.com/watch?v=jfKfPfyJRdk"
   ```

4. **yt-dlpを最新版に更新**
   ```bash
   # pipでインストールした場合
   pip install -U yt-dlp
   
   # パッケージマネージャーでインストールした場合
   sudo apt-get update && sudo apt-get upgrade yt-dlp  # Ubuntu/Debian
   brew upgrade yt-dlp  # macOS
   ```

### 通知音（ベル音）が鳴らない

**解決方法**:

1. **システムの音量を確認**: ミュートになっていないか確認
2. **端末のベル音を有効化**: 端末の設定で「ビープ音」や「ベル音」が有効になっているか確認
3. **代替の通知方法**: スクリプトに`notify-send`を追加して視覚的な通知も可能です

### スクリプトが実行できない

```bash
# 実行権限があるか確認
ls -l pomodoro_timer.sh

# 権限がない場合は付与
chmod +x pomodoro_timer.sh

# bashで直接実行
bash pomodoro_timer.sh
```

### BGMが停止しない

通常はスクリプト終了時やCtrl+Cで自動的に停止しますが、手動で停止する場合：

```bash
# mpvプロセスを確認
ps aux | grep mpv

# 強制終了
killall mpv
```

## 📚 学習ポイント

このスクリプトでは以下のbashテクニックを使用しています：

- **ユーザー入力**: `read -rp` でプロンプト付き入力
- **入力バリデーション**: 正規表現 `=~` で数値チェック
- **デフォルト値**: 空入力時の処理
- **配列**: `BGM_KEYWORDS=(...)` で複数の値を管理
- **ランダム選択**: `$RANDOM` を使った乱数生成
- **バックグラウンド実行**: `&` でプロセスをバックグラウンド化
- **プロセス管理**: `$!` でPIDを取得、`kill` で停止
- **シグナルハンドリング**: `trap` でCtrl+C時のクリーンアップ
- **コマンド存在チェック**: `command -v` で依存関係確認
- **関数**: コードの再利用と整理
- **算術展開**: `$((式))` で計算
- **条件分岐**: `[[ ]]` と `if/else`
- **ループ**: `while true` で無限ループ

## 📝 ライセンス

MIT License - 自由に使用・改変・配布してください

## 🤝 コントリビューション

バグ報告や機能リクエストはIssueでお願いします。
Pull Requestも歓迎します！

## 💡 今後の改善案

- [ ] デスクトップ通知の追加（`notify-send`）
- [ ] 統計機能（1日の完了セッション数を保存）
- [ ] 設定ファイルのサポート（`.pomodororc`）
- [ ] Spotify連携オプション
- [ ] カスタムBGM URL指定機能
- [ ] カラーテーマのカスタマイズ
- [ ] 長い休憩（4セッション後に15分休憩）の自動挿入

## 🙏 謝辞

このスクリプトは以下のオープンソースプロジェクトを使用しています：

- [yt-dlp](https://github.com/yt-dlp/yt-dlp) - YouTube動画のダウンロード
- [mpv](https://mpv.io/) - メディアプレイヤー

---

**Happy Focusing! 🚀🍅**
