// コマンドからnamespace生成
kubectl create ns database

// yamlファイルからnamespace生成
kubectl apply -f mysql-namespace.yaml

// dry-runからdeployment作成用のテンプレートをファイルに出力
kubectl create deploy mysql --image=mysql:5.7 --dry-run=client -o yaml > mysql-deployment.yaml

// yamlファイルからdeploymentを名前空間databaseに作成
kubectl apply -f mysql-deployment.yaml -n database

// Kubernetes クラスタ内で動作している MySQL コンテナにrootユーザでアクセス
kubectl exec -n database -it 動作しているポッド名 -- mysql -uroot -ppassword


// メモ
* 作成対象のapiVersionを確認する方法
kubectl api-resources | grep deployment
