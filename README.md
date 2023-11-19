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

☆  メモ
* 作成対象のapiVersionを確認する方法
```
kubectl api-resources | grep deployment
```
