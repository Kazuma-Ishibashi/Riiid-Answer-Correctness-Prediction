# Riiid-Answer-Correctness-Prediction
## 成績
- 期間：2020/12/7 〜 2021/1/7
- 順位：612th(19%)
- Public:0.783, Private:0.785 (AUC)
- model：LGBM

## コンペの概要

- TOEICの学習アプリを提供しているRiiidLabsという韓国のAIスタートアップが主催
- コンペティションでは、アプリユーザーが出された問題に正解できるかを、ユーザーの行動履歴から予測
- 本コンペではテストデータはTime-series APIというものを使って動的に与えられ、提出コード中で随時新しいデータが渡されていき、その都度予測する必要があるが、本コード内ではテストデータの予測は省略する。

## train_data カラムの説明
### row_id
行に対するID

### timestamp
ユーザの新規登録、該当レコードのイベント完了までのミリ秒単位の時間

### user_id
ユーザーID

### content_id
コンテンツID

### content_type_id
イベントが問題の場合は0、講義の場合は1

### task_container_id
問題または講義のバッチIDコード

### user_answer 
質問に対するユーザーの回答（講義の場合は-1）

### answered_correctly
ユーザーの回答が正解の場合「1」、不正解なら「0」(講義の場合は-1)

### prior_question_elapsed_time
ユーザーが前問題バンドルの各問題に回答するのにかかった平均時間（ミリ秒単位）

### prior_question_had_explanation
ユーザーが前問題バンドルに回答した後、説明と正しい回答を見たかどうか

## questions_data カラムの説明

### question_id: 
問題ID

### bundle_id:
大問題分類ID

### correct_answer:
回答

### part: 
TOEICテストのPart

### tags: 
問題の詳細なタグコード

## lectures_data カラムの説明

### lecture_id: 

講義ID

### part:

どのPartの講義か

### tag:
講義用のタグコード

### type_of:
講義目的の簡単な説明

## 作成した特徴量
### コンテンツごとの集計特徴
- 正解数、率、合計
- Partごとの正解率, 数
- ユーザーが解くのにかかった時間の平均
- 問題バッチ毎の正解率、数
- 解説の受講率　など

### ユーザーごとの集計特徴
- 正解数、率、合計
- Part毎の正解数、率、合計
- 同一問題への試行回数
- 講義、解説受講した数、率
- 時間のラグ　など
