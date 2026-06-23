### cloud native postgres 사용해보기

### helm 으로 설치하기
```bash
# 1. cnpg 공식 helm 저장소 추가하기
# https://cloudnative-pg.github.io/charts 를 가르키는 cnpg 이름의 helm 저장소를 local 에 추가
helm repo add cnpg https://cloudnative-pg.github.io/charts
# 추가한 저장소에 머가 있는지 받아오기 ( update 하기 )
helm repo update
# 저장소 목록 확인
helm repo ls
NAME    URL                                    
cnpg    https://cloudnative-pg.github.io/charts

# 설치하기 (Operator 중계자)
helm upgrade --install cnpg --namespace cnpg-system --create-namespace cnpg/cloudnative-pg
```

### 헬름 저장소는 원하는 이름으로 바로바로 추가할수있다 Operator 중계자는 진짜 postgres는 아니다

yaml 파일 spec instance 에 3 을적으면 알아서 primary, replica 나눠서 하고
스테이트 풀 셋도 적용을 자동으로 해준다..
혹시 primary 가 죽으면 replica가 자동으로 primary로 승격이된다 이런 동작도들어잇다..
포스트그레스가 사용할 pv가 필요한데.. nfs 에다가 만들어놓고 설정해서 설치할것이다..

### nfs 서버에 공유폴더 준비하기
```bash
./make-nfs.sh pv-postgres-1
./make-nfs.sh pv-postgres-2
./make-nfs.sh pv-postgres-3
```

### cnpg-cluster.yaml 파일과 init.yaml파일의 관계를 잘 생각하기

# pod 에 접속
```bash
kubectl exec -it my-pg-cluster-1 -- /bin/bash

```

### k8s 모니터링 툴 k9s 설치

#### ubuntu k9s 설치
```bash
wget https://github.com/derailed/k9s/releases/latest/download/k9s_Linux_amd64.tar.gz
tar -zxvf k9s_Linux_amd64.tar.gz
sudo mv k9s /usr/local/bin/
rm k9s_Linux_amd64.tar.gz LICENSE README.md
k9s
```