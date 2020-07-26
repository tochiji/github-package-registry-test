# github-package-registry-test
Github Packageにアップロードするテストしていきます

# 手順
### ①.npmrcファイルを作成

```
# .npmrcというファイルを作成し、下記記入
# 「/」以下はアカウント名かチーム名

registry=https://npm.pkg.github.com/tochiji
```

### ②トークンを取得
https://docs.github.com/ja/github/authenticating-to-github/creating-a-personal-access-token

必要な権限は `write:packages`。伴って必要な権限は自動的にチェックが入る。

### ③~/.npmrcにトークンを記入
```
# TOKENにアクセストークンを入れる。これでGithub Packageにアップロードできる

echo "//npm.pkg.github.com/:_authToken=TOKEN" >> ~/.npmrc
```

### ④package.jsonに、publishConfigを追加
```
{
  ...
  "publishConfig": {
    "registry":"https://npm.pkg.github.com/"
  },
  ...
}
```

### ⑤package.jsonのnameの頭に、@username（@organization）/を追加
```
"name": "@tochiji/github-package-registry-test"
```

### ⑥npm publish
下記コマンドでgithub repositoryのpackageに公開される
```
npm publish
```
