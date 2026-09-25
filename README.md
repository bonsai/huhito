# huhito

戸籍・系譜資料を管理するエージェント。

## Purpose

- GitHub とローカルにある戸籍関連資料を整理する
- 原資料、抽出データ、人物、出来事、親族関係を分離する
- 資料に基づく事実と推定（hypothesis）を分離する
- 古代から現代までの戸籍制度史を参照可能にする

## Data boundary

原本・個人情報を含む資料は原則ローカルで管理し、GitHubには公開可能な構造化データとメタデータだけを保存する。

## Initial model

`source → record → person/event/relation → hypothesis → review → export`

## Name

`huhito` は古代日本の戸籍・行政記録を想起させるエージェント名として採用する。
