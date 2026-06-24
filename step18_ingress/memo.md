```bash

# nginx-ingress-controller 를 배포할수있는 yaml 파일 다운로드하기
wget https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.8.2/deploy/static/provider/baremetal/deploy.yaml

# 파일 명 변경
mv deploy.yaml 04-ingress-controller.yaml

k apply -f 04 ... 해서 배포
```