## 공식 helm chart를 이용해서 argo cd 설치하기

```bash
# 1. ArgoCD 공식 레포지토리 등록
helm repo add argo https://argoproj.github.io/argo-helm

# 2. 업데이트
helm repo update

# 4. 설치할 ns 만들기
# kubectl create namespace argocd

# 5. helm 을 이용해서 설치하기
# helm install <배포의 이름>  <배포할 내용> -n <네임스페이스> -f <옵션정보를 담은 yaml>
helm install my-argocd argo/argo-cd -n argocd -f my-values.yaml

# 비밀번호 
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo

# 접속 주소 
kubectl get svc -n argocd

# helm으로 배포된 app 의 목록 확인
helm ls
helm ls -n <namespace>
helm ls -n argocd


# values.yaml 또는 소스코드를 수정 후에 다시 적용하기
# values.yaml을 수정하고 아래의 명령을 다시 실행해보기
---
# my-values.yaml

# ArgoCD 웹서버(UI)의 네트워크 설정 전달하기
server:
  service:
    type: LoadBalancer
  # https 외에 http로도 접속 가능하도록 
  extraArgs:
    - --insecure
--- 로 수정

helm upgrade my-argocd argo/argo-cd -n argocd -f my-values.yaml

# helm 으로 배포된 app 삭제하기
helm uninstall <name> -n <namespace>
helm uninstall my-argocd -n argocd
```