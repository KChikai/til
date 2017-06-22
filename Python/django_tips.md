# Django Tips

WebフレームワークDjango周りのTips． 基本的なコマンドや，WebAPIを作った時のメモ．

<br>


## 設計思想

MVCではない ･･･ 設計思想はMVCでと同じですが、モデル (Model)、テンプレート (Template)、ビュー (View)のMTV．

- Model ... Database に格納してあるデータ、および付随する処理
- Template ... テンプレートファイルによってデザインされた各ページのデザイン
- View ... リクエストがあった URI ごとに、どのページを見せるかを記述する処理

<br>


## Requirement

`pip install` でインストール可能．

```
django
django-admin
djangorestflamework
django-filter
markdown
```

<br>


## 作成手順

1. `django-admin startproject <project_name>`でプロジェクトが生成される． プロジェクトとは複数のアプリを管理する一つの箱のようなもの．

2. `manage.py`のディレクトリ内で`python manage.py startapp <app_name>`を実行． これにより，雛形ディレクトリが生成される．

3. `app_name/setting.py`の`INSTALLED_APPS`に`app_name`を追加 → `model.py`の設定が認識される． 同様に`INSTALLED_APPS`に`rest_framework`を追加する（REST APIを作成したい場合）． `setting.py`の`LANGUAGE_CODE`と`TIME_ZONE`を変更するなら変える(例：`‘ja’`, `‘Asia/Tokyo’`)

<br>


## REST API

#### GET

```
curl http://127.0.0.1:8000/app_name/hoge
```

#### SET

SETで数値を渡す場合は、apiのURL＋?+変数名=値&変数名２=値２　のような形にする．
↓こんな感じで呼び出す．（一例）

```
http://localhost:8000/api/set?task_name=名前&status=完了
```

<br>



## Database関連

### マイグレーションとは?

マイグレーションとは，プログラムやデータ，OSなどの環境やプラットフォームを移行，変換すること． Djangoの場合は `models.py` → Database への変換のことをマイグレーションと呼ぶ． migrationファイルを作成した後 migrate を実行すると，DBに変更が反映される．

```
python manage.py makemigrations
python manage.py migrate
```

<br>

### シリアライザーとは？

POSTやGETで受け取ったデータを処理して，modelに渡したり，受け取ったりするもの． 具体的には，モデルをJSONにマッピングする役割．

<br>

### データベースの削除
テーブル構造はそのまま，データのみ削除できる (スーパーユーザは登録し直す必要あり)
```
python manage.py flush --database=default
```

<br>

### データベース関連のエラー

データベース関連のエラーについてまとめる．

**Django dependencies reference nonexistent parent nodeのエラーについて**

前回のマイグレーションデータのカスが残っている時に発生するエラー．

残りカスを削除したのち再度マイグレーション生成する必要がある．

1. `__pycache__`を削除する
2. 0002_autoなんとかとかのmigrate files を削除
3. `python manage.py makemigrations`を実行

<br>

**no such table: 問題について**

`db.sqlite3`を直接シェル上からdropすると起こる．（データテーブル自体が消えるので当然であるが．．．）
makemigrate => migrateしても新しくテーブルは作成されない．
この時は，`db.sqlite`ファイルそのものを削除して，再度makemigrate => migrateすることで解決する．
（データベースが全部消えるので最終手段）

<br>

**SystemCheckError: System check identified some issues: エラーについて**

admin用pythonスクリプトのカラムネームの間違いにより起こった．
実際これが起こるとmigrate等が全くできないので注意．

<br>

**Foreign Key のネストデータが上手く表示されないケース**

一番詰まった．現状の解決策として，

データベースの消去，
外部キーのカラム名を手動で設定(db_column=)
tutorialどうりのネストデータに設定する
リードオンリーを忘れずに設定
modelをいじった時は注意（最悪もう一度データベースを作り直すとこから始めた方が良い場合がある）

これっていう解決策がわからない．
（コードを変えていないのに治るケースがあったので何かしらの前データのゴミが残っていた可能性がある）

<br>

**excludeしたい問題**

解決，DynamicSerializerクラスを定義してそれを使用する．
excludeしたいフィールドを投げると削ってくれる．

<br>
