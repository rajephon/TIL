
## minikube에서 LoadBalancer 타입 서비스 접속 테스트하기

```text
$ kubectl get svc
NAME                            TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
web-server-service              LoadBalancer   10.99.149.132   <pending>     3000:32468/TCP   13s
postgresql                      ClusterIP      10.100.8.251    <none>        5432/TCP         13s
postgresql-headless             ClusterIP      None            <none>        5432/TCP         13s
kubernetes                      ClusterIP      10.96.0.1       <none>        443/TCP          64m
```

- minikube에서 LoadBanacer 타입의 서비스를 생성하면 계속 `<pending>` 상태에 머물러있다.
- 이는 `LoadBalancer` 서비스가 [외부 클라우드 공급자가 지원](https://kubernetes.io/ko/docs/concepts/services-networking/service/#loadbalancer)하는 형태로 동작하기 때문이다.
- 미니쿠베에서는 `minikube service` 명령어를 활용하여 테스트할 수 있다.

```text
$ minikube service web-server-service
|-----------|--------------------|----------------------|---------------------------|
| NAMESPACE |        NAME        |     TARGET PORT      |            URL            |
|-----------|--------------------|----------------------|---------------------------|
| default   | web-server-service | web-server-port/3000 | http://192.168.49.2:32468 |
|-----------|--------------------|----------------------|---------------------------|
🏃  admin-web-server-service 서비스의 터널을 시작하는 중
|-----------|--------------------|-------------|------------------------|
| NAMESPACE |        NAME        | TARGET PORT |          URL           |
|-----------|--------------------|-------------|------------------------|
| default   | web-server-service |             | http://127.0.0.1:60807 |
|-----------|--------------------|-------------|------------------------|
🎉  Opening service default/web-server-service in default browser...
❗  Because you are using a Docker driver on darwin, the terminal needs to be open to run it.
```

### References
- [minikube에서 서비스 테스트 하기](https://bcho.tistory.com/1308)