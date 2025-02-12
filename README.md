# ngl-python-fastapi-template

https://chatgpt.com/share/67aa542f-dd0c-8013-a9dd-5510927e651c

## ローカル端末上での作業

ocプロジェクト名であるche-kube-admin-devspaces-8h5s6rは適宜読み替えること

```bash
cp -p continue.example/config.json .
# OpenAIのAPIキーを設定する, DevSpacesのワークスペースで/home/user/.continueにコピーして利用する
oc create secret generic continue-config-secret \
  --from-file=config.json=config.json \
  -n che-kube-admin-devspaces-8h5s6r
#自動でマウントするために以下を実行
oc label secret continue-config-secret \
  controller.devfile.io/mount-to-devworkspace='true' \
  controller.devfile.io/watch-secret='true' \
  -n che-kube-admin-devspaces-8h5s6r
# oc apply -f secrect.yaml

  oc get secret continue-config-secret -o jsonpath='{.data.config\.json}' -n your-namespace | base64 --decodes
```

作成したシークレットを削除したい場合は以下を実行する

```bash
#oc delete secrets/continue-config-secret -n che-kube-admin-devspaces-8h5s6r
```

##　DevSpaces上での実行

今のところは自分でTask Runしないとconfig.jsonを上書きできない
Run task　copyconfig

```bash
pip install -r requirements.txt
uvicorn server:app --reload
```

## ローカル端末から動作確認

```bash
#Pod名の確認
oc get pod 
oc port-forward -n [ocプロジェクト名] pod/[Pod名] 8000:8000

#実行例
oc port-forward -n che-kube-admin-devspaces-8h5s6r pod/workspace7082c4664770461c-7b65549556-7q8jz 8000:8000

#別ターミナルで以下を実行する
curl http://localhost:8000
```

# 参考

https://docs.redhat.com/ja/documentation/red_hat_openshift_dev_spaces/3.18/html/user_guide/using-credentials-and-configurations-in-workspaces#mounting-secrets





ls /etc/secret/continue-config-secret/.continuerc.json

cp -p /etc/secret/continue-config-secret/.continuerc.json /projects/.



今のところは自分でTask Runしないと上書きできない