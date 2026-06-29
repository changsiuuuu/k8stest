## argocd 설치해서 사용해 보기

```bash
# 1. 아르고 CD를 위한 네임스페이스 생성
kubectl create namespace argocd

# 2. 아르고 CD를 다운받지 않고 즉석해서 바로 설치
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.11.0/manifests/install.yaml

# 3. 설치 후에 svc 목록 확인
kubectl get svc -n argocd

# 4. 서비스 타입 로드밸런서로 변경
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'

# 5. 접속 주소확인
kubectl get svc argocd-server -n argocd -w
```

```bash
# 유저네임은 admin인데 비번은 따로 명령어로 알아내야한다
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo

"게속바뀐다"
```

### 깃헙 사용할 준비
window 의 .ssh 폴더안에서 만들어둔 id_ed25519 파일을 여기 .ssh/에 넣기
config 파일 작성 권한 설정

```bash
#삭제하는법
kubectl delete -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.11.0/manifests/install.yaml
```