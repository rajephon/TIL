# 로컬 컴퓨터에서 k3s 클러스터 접속하기

클러스터에 사용되는 TLS 인증서에 [Subject Alternative Name](https://en.wikipedia.org/wiki/Subject_Alternative_Name)에 인스턴스에 배정된 공인IP 혹은 도메인 주소가 추가되어야 합니다.

이를 위해 k3s의 `--tls-san` 옵션에 값으로 지정해줘야 합니다.

## 방법 1. 설치시 시정하기

```sh
curl -sfL https://get.k3s.io | INSTALL_K3S_EXEC="--tls-san x.x.x.x" sh -s -
```

`INSTALL_K3S_EXEC` 환경변수로 인스턴스에 배정된 공인IP를 설정합니다.

## 방법 2. 이미 설치되었으면 설정을 지정해주기

k3s가 이미 설치했으면, `/etc/systemd/system/k3s.service` 파일의 다음의 부분을 수정합니다.

```text
ExecStart=/usr/local/bin/k3s \
    server \
       '-tls-san=x.x.x.x' \  ## 공인IP 설정
```

설정을 반영하기 위해 `dynamic-cert.json` 를 재생성하게 해주고, k3s 를 재시작합니다.

```bash
kubectl -n kube-system delete secrets/k3s-serving
sudo mv /var/lib/rancher/k3s/server/tls/dynamic-cert.json /tmp/dynamic-cert.json
sudo systemctl restart k3s
```

### 레퍼런스

- [K3s Server Configuration#listeners](https://docs.k3s.io/reference/server-config#listeners)
- [Remote kubectl x509: certificate is valid for 127.0.0.1 / ferllings's answer](https://github.com/k3s-io/k3s/issues/1381#issuecomment-582291774)
- [Remote kubectl x509: certificate is valid for 127.0.0.1 / vast0906's answer](https://github.com/k3s-io/k3s/issues/1381#issuecomment-1220219450)
- [k3s 시리즈 - 간단하게 Kubernetes 환경 구축하기](https://si.mpli.st/dev/2020-01-01-easy-k8s-with-k3s/)