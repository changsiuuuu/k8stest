### helm chart 저장소에 있는 chart 활용하기

```bash
helm repo add <저장소이름> <저장소깃헙페이지>
helm repo add my-repo https://changsiuuuu.github.io/mychart
helm update
helm search repo my-repo
NAME                    CHART VERSION   APP VERSION     DESCRIPTION                    
my-repo/market-app      0.1.0                           market app helm chart for kuber
my-repo/member-app      0.1.1                           fastapi member application
# 바로 install 말고 local 로 다운로드해서 커스터마이징도 할 수 있다..
helm pull my-repo/market-app 
# 그럼 동폴더에 market-app-0.1.0.tgz 파일이 다운로드된다
# 압축된 상태론 쓸 수 없으니 압축을 푼다
tar -zxvf <압축파일명>
tar -zxvf market-app-0.1.0.tgz
# 그럼 폴더가 생기면서 압축 풀린 결과물이 생긴다.. 그럼 커스텀이 가능

# tgz 파일을 생성하지 않고 바로 압축을 해제해서 원하는 경로에 넣을수도 있다..
# charts라는 폴더 만들고..
helm pull my-repo/member-app --untar --untardir ./charts
```