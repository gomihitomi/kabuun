# kabuun
bunの遊び場です

## 必要な物
- Dockerが動く環境
- GitHubからクローン出来る環境
- VSCode
  - DevContainer

### 動かし方
1. GitHubからクローンしたソースコードを、VSCodeで開く
```bash
git clone https://github.com/gomihitomi/kabuun
cd kabuun
code .
```

2. VSCodeから開発コンテナで開く
```markdown
VSCode で コマンドパレット(Shift + Ctrl + P) を開く
`コンテナーで再度開く(Reopen in Container)` を選択
```

3. 依存解決、開発コンテナ立てる、デプロイする
```markdown
// TODO
```


### その他
- よく使うDockerのコマンド
```bash
docker compose ps
docker compose ps -a
dokcer compose build --no-cache
docker compose build --progress=plain
docker compose up -d
docker compose down
docker logs -f {container_name}
```

- WSL環境でパーミッション周りがおかしくなった
```bash
# ファイル作成したホストと、Dockerのユーザ、グループが違うのが原因。
# エラーが出たユーザで上書きすれば良いはず（よくはないね）
sudo chown -R {user}:{group} .
```

- なんか色々してたら立ち上げに失敗した
```bash
# 大した物入ってないので一旦コンテナ潰して作り直した方が早い
# 全コンテナ削除
docker rm -f `docker ps -a -q`
```
