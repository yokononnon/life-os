# GitHub・Obsidian 接続復旧手順

## 症状

Obsidian GitでPush/Pullすると

- Username
- Password

を聞かれる。

## 原因

リポジトリの remote が HTTPS になっている。

確認

```bash
git remote -v
```

NG例

```text
origin https://github.com/yokononnon/life-os (fetch)
origin https://github.com/yokononnon/life-os (push)
```

OK例

```text
origin git@github.com:yokononnon/life-os.git (fetch)
origin git@github.com:yokononnon/life-os.git (push)
```

---

## 復旧手順

### 1. SSH URLへ変更

GitHub

Code → SSH

を選択してURLをコピー。

```text
git@github.com:yokononnon/life-os.git
```

変更

```bash
git remote set-url origin git@github.com:yokononnon/life-os.git
```

---

### 2. 確認

```bash
git remote -v
```

SSHになっていればOK。

---

### 3. SSH認証確認

```bash
ssh -T git@github.com
```

成功すると

```text
Hi yokononnon! You've successfully authenticated, but GitHub does not provide shell access.
```

と表示される。

---

### 4. Push確認

```bash
git push
```

```text
Everything up-to-date
```

または

```text
Enumerating objects...
```

が表示されれば正常。

---

## 注意

リポジトリを作り直すとHTTPSに戻ることがある。

その場合はこの手順を実施する。

---

## 今回の原因

リポジトリを新しく作成した際にremote URLが

```
https://github.com/...
```

になっていた。

SSHへ変更することで解決。