# Django Tips

WebフレームワークDjango周りのTips．
基本的なコマンドや，WebAPIを作った時のメモ．

<br>

## 設計思想

MVCではない ･･･ 設計思想はMVCでと同じですが、モデル (Model)、テンプレート (Template)、ビュー (View)のMTV．

- Model　…　Database に格納してあるデータ、および付随する処理
- Template　…　テンプレートファイルによってデザインされた各ページのデザイン
- View　…　リクエストがあった URI ごとに、どのページを見せるかを記述する処理


<br>

## Requirement

`pip install` でインストール可能．

    django
    django-admin
    djangorestflamework
    django-filter
    markdown

<br>

## 作成手順

1. `django-admin startproject <project_name>`でプロジェクトが生成される．
プロジェクトとは複数のアプリを管理する一つの箱のようなもの．

2. `manage.py`のディレクトリ内で`python manage.py startapp <app_name>`を実行．
これにより，雛形ディレクトリが生成される．


3. `app_name/setting.py`の`INSTALLED_APPS`に`app_name`を追加　→　model.pyの設定が認識される．
同様に`INSTALLED_APPS`に`rest_framework`を追加する（REST APIを作成したい場合）．
`setting.py`の`LANGUAGE_CODE`と`TIME_ZONE`を変更するなら変える(例：`‘ja’`, `‘Asia/Tokyo’`)

<br>

## Database Migration

**マイグレーションとは?**
<p style="text-indent:1em">
マイグレーションとは，プログラムやデータ，OSなどの環境やプラットフォームを移行，変換すること．
Djangoの場合は `models.py` → Database への変換のことをマイグレーションと呼ぶ．
migrationファイルを作成した後 migrate を実行すると，DBに変更が反映される．
</p>

    python manage.py makemigrations
    python manage.py migrate

<br>
