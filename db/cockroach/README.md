# Cockroach DB

## CockroachDB Serverless (beta) 프리티어

- CockroachDB는 현재 **신용카드 번호 없이** 프리티어 서비스를 사용할 수 있다.
- 5GiB 스토리지, 최대 250M RUs 성능
- 최대 5개 클러스터 생성이 가능하다.
- Google, AWS로 Cloud provider를 고를 수 있다.
  - Google은 Jurong West, Iowa, St.Ghislain 리전
  - AWS는 Singapore, Oregon, Ireland 리전
- 옵션을 선택 후 클러스터를 생성하면,
  - OS에 알맞게 cockroach 바이너리 파일과 root 인증서를 내려받을 수 있는 명령어를 제공받는다.
  ```sh
  curl https://binaries.cockroachdb.com/cockroach-v21.2.0.darwin-10.9-amd64.tgz | tar -xz; sudo cp -i cockroach-v21.2.0.darwin-10.9-amd64/cockroach /usr/local/bin/
  curl --create-dirs -o $HOME/.postgresql/root.crt -O https://cockroachlabs.cloud/clusters/foo-bar-nyan-cat/cert
  ```
  - 가이드에 따라 바이너리와 인증서를 /usr/local/bin/, $HOME/.postgresql 디렉토리에 설치하거나 적절한 곳에 내려받는다.
  - DB 연결
  ```sh
  cockroach sql --url 'postgresql://[user]:[pw]@[host]:[port]/defaultdb?sslmode=verify-full&sslrootcert='$HOME'/.postgresql/root.crt&options=[options]'
  ```
  - DataGrip도 지원하고 있으므로, 예시로 주어진 명령어대로 적절한 옵션 세팅을 통해 사용할 수 있다.

### Reference

- https://www.cockroachlabs.com/lp/serverless/
- [CockroachDB Serverless (beta) FAQs](https://www.cockroachlabs.com/docs/cockroachcloud/serverless-faqs.html#what-are-the-usage-limits-of-cockroachdb-serverless-beta)