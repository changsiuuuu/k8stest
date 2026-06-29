### 프로메테우스, 그라파나 스택 설치
```bash
# 1. 프로메테우스 커뮤니티 헬름 레포지토리 등록
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

# 2. 메뉴판 최신화 (아까  명령어!)
helm repo update

# 3. 모니터링 전용 방(Namespace) 생성
kubectl create namespace monitoring

# 4. 커스텀 변수(my-values.yaml)를 적용해서 설치!
helm install my-kube-prometheus prometheus-community/kube-prometheus-stack \
  -n monitoring \
  -f my-values.yaml

# 4. 변수를 수정하고 다시 적용하고싶으면 helm upgrade로 실행
helm upgrade my-kube-prometheus prometheus-community/kube-prometheus-stack \
  -n monitoring \
  -f my-values.yaml

# 확인하기
helm ls -n monitoring
k get pod,svc -n monitoring
```

### 웹브라우저로 접속해보기 NodePort 32000 그라파나, 32100 프로메테우스

### 그라파나를 servicetype Loadbalancer로 바꾸고 업그레이드해보기
```bash
grafana:
  adminPassword: "admin" # 비밀번호를 쉽게 고정
  service:
    type: LoadBalancer # 또는 LoadBalancer

helm upgrade my-kube-prometheus prometheus-community/kube-prometheus-stack \
  -n monitoring \
  -f my-values.yaml
```