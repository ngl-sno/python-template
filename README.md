# python-template

https://chatgpt.com/share/67aa542f-dd0c-8013-a9dd-5510927e651c

/home/user/.continue

```bash
cp -p .continue.example/config.json .
oc create secret generic continue-config-secret \
  --from-file=config.json=config.json \
  -n che-kube-admin-devspaces-8h5s6r
# oc apply -f secrect.yaml

  oc get secrets -n your-namespace
  oc get secret continue-config-secret -o jsonpath='{.data.config\.json}' -n your-namespace | base64 --decode
oc delete secrets/continue-config-secret -n che-kube-admin-devspaces-8h5s6r
```

https://docs.redhat.com/ja/documentation/red_hat_openshift_dev_spaces/3.3/html/user_guide/mounting-secrets#mounting-secrets

https://docs.redhat.com/ja/documentation/red_hat_openshift_dev_spaces/3.18/html/user_guide/using-credentials-and-configurations-in-workspaces#mounting-secrets





ls /etc/secret/continue-config-secret/.continuerc.json

cp -p /etc/secret/continue-config-secret/.continuerc.json /projects/.



今のところは自分でTask Runしないと上書きできない