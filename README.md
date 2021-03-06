# mlops_env_sample
MLOps等で利用するML環境サンプル

## 使い方

### ビルド&起動

1. ビルド `$ docker-compose -f docker-compose.yml build`
   - キャッシュを使わない場合は `--no-cache`オプションを付加
2. 起動 `$ docker-compose -f docker-compose.yml up -d`
3. `http://localhost:8888` にアクセスすると，jupyterlab認証画面が出る
   - 今回はサンプル用にパスワードを`aaaa`と設定．この文字列を入力して実行すればログインできる．

### 終了

`docker-compose -f docker-compose.yml down`

### AWS CLI 環境設定

`mlops_env_sample`ディレクトリ配下に`/env_settings/.env`を作成し，以下の通り環境変数を設定する．

```.env
# develop環境
AWS_ACCESS_KEY_ID_DEV={devlop環境のアクセスキーID}
AWS_SECRET_ACCESS_KEY_DEV={devlop環境のシークレットキーID}

# staging環境
AWS_ACCESS_KEY_ID_STG
AWS_SECRET_ACCESS_KEY_STG

# production環境
AWS_ACCESS_KEY_ID_PRD
AWS_SECRET_ACCESS_KEY_PRD

REGION
```

### （Optional）ECRにbuildしたコンテナイメージをUpload

SageMakerやCircleCIのベースイメージ等をECRに登録しておきたい場合．

`mlops_env_sample`ディレクトリ配下の`push_to_ecr.sh`を実行

```
$ chmod +x push_to_ecr.sh
$ ./push_to_ecr.sh {profile名(指定しない場合は'default')} {コンテナイメージのtag名}
```