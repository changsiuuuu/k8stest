# 1. 헬름 공식 GitHub에서 최신 압축 파일 다운로드 
curl -LO https://get.helm.sh/helm-v3.14.2-linux-amd64.tar.gz

# 2. 압축 해제
tar -zxvf helm-v3.14.2-linux-amd64.tar.gz

# 3. 압축 푼 폴더 안에서 'helm' 실행 파일만 골라서 시스템 실행 경로로 이동
sudo mv linux-amd64/helm /usr/local/bin/helm

# 4. 다운로드했던 임시 파일 삭제
rm -rf id linux-amd64 helm-v3.14.2-linux-amd64.tar.gz

## 만든 헬름차트 사용해보기

```bash
# templates 파일을 이용해서 yaml 문서 얻기
helm template team1-env ./dev-tenant-maker > team1-result.yaml

# 혹은 템플릿을 해석한 결과물을 바로적용할라면 (apply)

helm install team1-env ./dev-tenant-maker 

helm list

helm uninstall   <배포 이름 >
```