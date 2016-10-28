# git-practice
朝食と昼食まとめ用リポジトリ

- [朝食リポジトリ](https://github.com/matsuo-y/git-practice-breakfast)
- [朝食本番環境(github)](https://matsuo-y.github.io/git-practice-breakfast/)
- [昼食リポジトリ](https://github.com/matsuo-y/git-practice-lunch)
- [昼食本番環境(github)](https://matsuo-y.github.io/git-practice-lunch/)

- [waffleかんばん](https://waffle.io/matsuo-y/git-practice)

# ブランチについて

## ブランチの種類

- master branch：本番環境にデプロイするコードを格納するブランチ
- staging branch：staging環境にデプロイするコードを格納するブランチ
- issue branch：staging branchを起点とし、issueの開発を実装したコードを格納するブランチ
- issue child branch：issue branchを起点とし、issueの開発に関する小さな単位の機能を実装したコードを格納するブランチ

## ブランチの初期設定

- master branch
 - github.com リポジトリの設定で、誰かが誤って削除しないように、force pushしないように、プロテクトする
 - github.com リポジトリの設定で、誰かが直接コミットしないように、PRを通して、マージするように設定する

- staging branch
 - github.com リポジトリの設定で、誰かが誤って削除しないように、force pushしないように、プロテクトする
 - github.com リポジトリの設定で、誰かが直接コミットしないように、PRを通して、マージするように設定する

## ブランチのマージルール
- master branchは、staging branchからのPRのみを受け付ける
- staging branchは、issue branchからのPRのみを受け付ける
- issue branchは、issue child branchからのPRのみを受け付ける

## ブランチの運用ルール
- staging branch から、 issue branch を分岐する(checkout)
- staging branchにマージコミットが発生した場合、存在するissue branch はstaging branchの変更分のコミットを取り込む（マージする）：　当分はrebaseはしない

- issue branch から、issue child branch を分岐する (checkout)
- issue branchにマージコミットが発生した場合、存在するissue child branch はissue branchの変更分のコミットを取り込む（マージする）：　当分はrebaseはしない

# 各リポジトリについて

## 朝食リポジトリ
`アプリ内書店の開発のように、リリースまでの開発期間が長いブランチ戦略`
- issue作成者
 - 朝食リポジトリでのissue作成
 - issueブランチへのPRレビュー(最低1回は修正依頼を出す)
 - staging・masterブランチへのPR作成
- branch作成者
 - issueが発行された後、stagingブランチからissueブランチを作成
- 開発担当者(朝食報告、2名)
 - issueブランチから作業用ブランチを作成し、issueブランチへのPRを作成
- 検収担当者
 - 開発担当者が、issueブランチをもとにstagingブランチへのPRを作成し、issueブランチをデプロイした結果を確認した後、検収担当者が、stagingブランチへのPRをレビューし、マージする
- リリース担当者
 - stagingブランチをもとにmasterブランチへのPRを作成し、stagingブランチをデプロイした結果を確認した後、masterブランチへのPRをマージする
 - masterブランチへマージ後にデプロイタスクを実行(今回はherokuやgithubが自動実行)し、releases/tagsの設定を行う

## 昼食リポジトリ
`開発内容を即時リリースするように、リリースまでの開発期間が短いブランチ戦略`
- issue作成者
 - 昼食リポジトリでのissue作成
 - stagingブランチへのPRレビュー(最低1回は修正依頼を出す)
 - masterブランチへのPR作成
- branch作成者
 - issueが発行された後、stagingブランチからissueブランチを作成
- 開発担当者(昼食報告、1名)
 - issueブランチで作業を行い、stagingブランチへのPRを作成
- 検収担当者
 - 開発担当者が、issueブランチをもとにstagingブランチへのPRを作成し、issueブランチをデプロイした結果を確認した後、検収担当者が、stagingブランチへのPRをレビューし、マージする
- リリース担当者
 - stagingブランチをもとにmasterブランチへのPRを作成し、stagingブランチをデプロイした結果を確認した後、masterブランチへのPRをマージする
 - masterブランチへマージ後にデプロイタスクを実行(今回はherokuやgithubが自動実行)し、releases/tagsの設定を行う

__ ※昼食でのstagingブランチへのPRレビュー順 __

- 【issueブランチ】
 - ↓[issue作成者レビュー(PRでレビューした旨のコメント記載)]
 - ↓[検収担当者レビュー(PRマージ実行)]
- 【stagingブランチ】

# herokuについて

## 朝食

- review app環境(対象ブランチ：matsuo-y/git-practice-breakfastのPRマージ元issueブランチ)：https://git-practice-breakfast-pr-{N}.herokuapp.com/
- ステージング環境(対象ブランチ：matsuo-y/git-practice-breakfastのstaging)：https://staging-git-practice-breakfast.herokuapp.com/
- 本番環境(対象ブランチ：matsuo-y/git-practice-breakfastのmaster)：https://git-practice-breakfast.herokuapp.com/

## 昼食

- review app環境(対象ブランチ：matsuo-y/git-practice-lunchのPRマージ元issueブランチ)：https://git-practice-lunch-pr-{N}.herokuapp.com/
- ステージング環境(対象ブランチ：matsuo-y/git-practice-lunchのstaging)：https://staging-git-practice-lunch.herokuapp.com/
- 本番環境(対象ブランチ：matsuo-y/git-practice-lunchのmaster)：https://git-practice-lunch.herokuapp.com/
