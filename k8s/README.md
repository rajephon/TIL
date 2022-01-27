# Kubernetes

## 쿠버네티스 설치 도구 및 서비스와 특징 비교

- Docker for Mac/Windows, Minikube
  - 1개의 노드에서 설치 및 사용
  - 간편하게 로컬에서 테스트 가능
  - 일부 기능 제한될 수 있음
- GKE, EKS 등 관리형 서비스
  - 설치 필요없음
  - 플랫폼 종속 기능 사용 가능(예: LB, Persistent Storage, 등)
  - 다소 비용 증가
- kubespray, kubeadm
  - 온프레미스 환경에서도 설치 가능
  - 클라우드 인프라에서도 설치 가능
  - 관리 어려울 수 있음
- kops
  - 특정 클라우드 플랫폼에서도 쉽게 설치 가능
  - 서버, 네트워크 등 각종 인프라도 자동으로 프로비저닝


### References

- [시작하세요! 도커/쿠버네티스](https://book.naver.com/bookdb/book_detail.nhn?bid=16850447)