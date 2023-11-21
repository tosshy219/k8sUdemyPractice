// コマンドからnamespace生成
```
kubectl create ns database
```

// yamlファイルからnamespace生成
```
kubectl apply -f mysql-namespace.yaml
```

// dry-runからdeployment作成用のテンプレートをファイルに出力
```
kubectl create deploy mysql --image=mysql:5.7 --dry-run=client -o yaml > mysql-deployment.yaml
```

// yamlファイルからdeploymentを名前空間databaseに作成
```
kubectl apply -f mysql-deployment.yaml -n database
```

// Kubernetes クラスタ内で動作している MySQL コンテナにrootユーザでアクセス
```
kubectl exec -n database -it 動作しているポッド名 -- mysql -uroot -ppassword
```

// サービスを作成するyamlを作成
```
kubectl create service サービスのタイプ mysql --tcp=3306 --dry-run=client -o yaml > mysql-service.yaml
```

// yamlからサービスを名前空間databaseに作成
```
kubectl apply -f mysql-servicel.yaml -n database
```

// sample-appのdeployment作成yamlファイル作成
```
kubectl create deployment sample-app --image=ghcr.io/nakamasamoto/fastapi-sample:v1.0 --dry-run=client -o yaml > sample-app-deployment.yaml
```

// env.txtを利用しconfigmapを作成するyamlファイルを作成
```
kubectl create cm sample-app --from-env-file=env.txt --dry-run=client -o yaml > sample-app-configmap.yaml
```

// mysqlパスワードを格納したsecretを作成するyamlファイルを作成
```
kubectl create secret generic sample-app --from-literal=MYSQL_PASSWORD=password --dry-run=client -o yaml > sample-app-secret.yaml
```

// 特定のnamespaceにまとめてyamlファイルからリソース作成
```
kubectl apply -f sample-app-deployment.yaml,sample-app-configmap.yaml,sample-app-secret.yaml -n $namespace
```


☆  メモ
* 作成対象のapiVersionを確認する方法
```
kubectl api-resources | grep deployment
```
