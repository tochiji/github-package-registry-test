# github-package-registry-test
![Node.js Package](https://github.com/tochiji/github-package-registry-test/workflows/Node.js%20Package/badge.svg)  

Github Packageにアップロードするテストしていきます

## パッケージアップロード手順
### ①.npmrcファイルを作成

```
# .npmrcというファイルを作成し、下記記入
# 「https://npm.pkg.github.com/」以下はアカウント名かチーム名

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

### ④package.jsonに「publishConfig」を追加
```
{
  ...
  "publishConfig": {
    "registry":"https://npm.pkg.github.com/"
  },
  ...
}
```

### ⑤package.jsonの「name」の頭に@username（@organization）/を追加
```
"name": "@tochiji/github-package-registry-test"
```
これがpackageの名前になる。⑥のrepositoryの名前と合わせる必要はない。

### ⑥package.jsonの「repository」の内容がgitのレポジトリとして正しいURLか確認。なければ追加
```
"repository": "https://github.com/tochiji/github-package-registry-test.git"
```
ここで指定したレポジトリに、パッケージがアップロードされる。

### ⑦npm publish
下記コマンドで、ローカルの内容がgithub repositoryのpackageに公開される
```
npm publish
```

## 注意事項
### publishされる内容

`npm publish`すると、現在ローカル作業中のブランチの内容がそのままpackageとしてpublishされる。  
githubのレポジトリは関係ない。ローカルで適当に変更したものをpublishすると、それがそのまま公開される。



## パッケージ利用手順
### ①利用したいプロジェクト内で.npmrcファイルを作成
```
# .npmrcというファイルを作成し、下記記入
registry=https://npm.pkg.github.com/tochiji
```
※参考：[アカウントやチームを複数追加する場合の書き方](https://docs.github.com/ja/packages/using-github-packages-with-your-projects-ecosystem/configuring-npm-for-use-with-github-packages#installing-packages-from-other-organizations)

### ②トークンを取得
https://docs.github.com/ja/github/authenticating-to-github/creating-a-personal-access-token

必要な権限は `read:packages`。伴って必要な権限は自動的にチェックが入る。

### ③~/.npmrcにトークンを記入
```
# TOKENにアクセストークンを入れる。これでGithub Packageにアップロードできる

echo "//npm.pkg.github.com/:_authToken=TOKEN" >> ~/.npmrc
```

### ④npm install PACKAGE
```
npm install @tochiji/github-package-registry-test
```

これでpackageを利用できます。
