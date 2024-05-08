# GitHubFlow

##　個人メモ

- checkout ブランチの移動
- -b ブランチの作成
- -D ブランチの削除
- -m メッセージの付与
- -u アップストリームの設定

## 1. 初期ブランチ構築（スクラムマスター）

- ローカルリポジトリで初期環境構築
- リモートリポジトリに main ブランチ作成
- ローカルリポジトリのブランチ名を main に変更

  ```sh
  $ git branch -m master main
  ```

- ローカルリポジトリで initial commit してリモートへプッシュ

  ```sh
  $ git add .
  $ git commit -m "initial commit"
  $ git remote add origin git@github.com:hfujiyos/gatsbyjs-site.git
  $ git push -u origin main
  ```

- リモートリポジトリにプロジェクト作成
- リモートリポジトリのプロジェクト設定

  ```
  プルリクエストがマージされた後、ヘッドブランチを自動的に削除
  ☑︎Automatically delete head branches
  ```

## 2. イシュー定義（レビュア）

- リモートリポジトリにイシューを作成して開発者をアサイン

  ```
  Add login mock
  Fix login logic
  ```

## 3. チケット駆動開発（開発者）

- ローカルリポジトリで main ブランチの最新のソースをプル

  ```sh
  mainブランチに切替
  $ git checkout main

  mainブランチの最新ソースをリモートリポジトリからプル
  $ git pull
  ```

- ローカルリポジトリに feature ブランチを切る

  ```sh
  featureブランチを新規作成してブランチ切替
  $ git checkout -b feature/fixLoginLogic
  ```

- ローカルリポジトリに feature ブランチで、コーディング / コミット / プッシュ

  ```sh
  開発時にはコミット
  $ git add .
  $ git commit -m "Fix login logic"

  featureブランチをリモートリポジトリへプッシュ
  $ git push origin HEAD
  ```

- リモートリポジトリの feature ブランチを、リモートリポジトリの main ブランチへマージ依頼するプルリクエスト

  ```
  マージする際にイシューもクローズするコメント付与
  $ close #9
  ```

## 4. コードレビュー（レビュア）

- レビュアにて、コードレビュー / 承認

- レビュアにて、main ブランチへマージ

## 5. 後工程（開発者）

- マージ後の main ブランチを取得する
- ローカルリポジトリで main ブランチの最新のソースをプル

  ```sh
  mainブランチに切替
  $ git checkout main

  mainブランチの最新ソースをリモートリポジトリからプル
  $ git pull
  ```

- ローカルリポジトリの不要ブランチ削除

  ```sh
  現在のブランチがmainであるか確認
  $ git branch
    feature/funcE
  * main

  ローカルリポジトリの不要ブランチを削除
  $ git branch -D feature/funcE

  不要ブランチが削除されていることを確認
  $ git branch
  * main
  ```

## 【番外編】Git 作業にミスしたとき

### 直前にコミットしたメッセージを変更する

- 直前コミットのメッセージのみを変更する

  ```sh
  $ git add -A
  $ git commit -m "htmlを修正"
  #あっ　今のコミット内容、cssの修正だった！書き直したい…！
  $ git commit --amend -m "cssを修正"
  #これで直前のコミットが更新されました！
  ```

### コミットの内容を取り消して無かったことにして最初からやり直したい

- 作業ディレクトリ

  - 変更・作成したもの全てリセットされる（直前のコミット状態になる）

- ステージングエリア

  - アンステージされる

  ```sh
  直前のコミットの状態に戻る
  $ git reset --hard HEAD
  ```
