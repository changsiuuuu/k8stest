### hello/memo.md

kubectl get nodes


pod1.yaml 에 정의된대로 만들겠다
kubectl apply -f pod1.yaml

kubectl get pod
kubectl get pod -o wide

curl <ip주소>
ping -c 3 <ip주소>

kubectl delete pod nginx-pod


# host의 8888 port를 pod 의 80 port로 연결해주는 NodePort 서비스 만들기
kubectl expose pod nginx-pod --type=NodePort --name=nginx-pod-svc --port=8888 --target-port=80 \
--labels="color=blue"

kubectl get svc nginx-pod-svc
나온 포트 172.16.8.10:32483  하니깐 접속이된다..

모든 노드에 대해서 접속이된다
http://172.16.8.11:32483/
http://172.16.8.12:32483/

kubectl expose pod nginx-pod --type=NodePort --name=nginx-pod-svc --port=8888 --target-port=80 \
--labels="color=blue" 이것도 yml 문서로 할수있는데
랜덤배정되는 포트를 정할수도있다 


kubectl delete pod <pod명>
kubectl delete -f <yaml명>

실습 후 vmware 를 끌때 
master node를 먼저 끄고 -> node1, node2를 끈다

다시 vmware를 켤때
node1, node2를 먼저 켜고 -> master node를 킨다.