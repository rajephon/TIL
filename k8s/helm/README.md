## bitnami PostgreSQL 초기화 sql 등록

- values.yaml 의 `initdbScripts`, `initdbScriptsConfigMap`, `initdbScriptsSecret` 활용
- 직접 등록
```yaml
postgresql: 
  initdbScripts:
    init-mydb.sql: |
      CREATE USER abc WITH PASSWORD 'abc';
      CREATE DATABASE mydb;
      GRANT ALL PRIVILEGES ON DATABASE mydb TO abc;
```
- configMap + sql 파일 활용
```bash
kubectl create configmap initdb-schema --from-file ./initdb/0-schema.sql --kubeconfig=${HOME}/.kube/config
```

```yaml
postgresql:
  initdbScriptsConfigMap: initdb-schema
```



## References
- [PostgreSQL Helm Chart: SQL scripts from `initdbScripts` won't be executed](https://giters.com/bitnami/charts/issues/8427#issuecomment-997424905)
- [bitnami PostgreSQL chart](https://github.com/bitnami/charts/tree/master/bitnami/postgresql)