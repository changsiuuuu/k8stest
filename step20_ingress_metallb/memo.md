### ingress-controller.yaml 의 365 번째 line 수정

```yaml
  selector:
    app.kubernetes.io/component: controller
    app.kubernetes.io/instance: ingress-nginx
    app.kubernetes.io/name: ingress-nginx
  type: LoadBalancer # defalut는 NodePort
```

### metallb 를 배포후에 먼저 대문 서비스 간판 조회
```bash

kubectl get svc -n ingress-nginx
[user1@master step20_ingress_metallb]$ kubectl get svc -n ingress-nginx
NAME                                 TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)                      AGE
ingress-nginx-controller             LoadBalancer   10.108.87.232   172.16.8.30   80:31396/TCP,443:30301/TCP   21m
ingress-nginx-controller-admission   ClusterIP      10.110.42.78    <none>        443/TCP                      21m
```

-- 08 ingress-rule 을 본다

http paths 해서 경로로 분기를 하고있다

  ingressClassName: nginx
  rules:
    - host: example.com
      http:
        # nginx 는 L7 장비라서 요청경로, 요청 URL 등의 정보를 모두 인식할수있다
        paths:

이부분에 
    - host: example.com 추가

이후 윈도우에서..

nodepad를 관리자권한으로 실행
파일 열기 경로 C:\Windows\System32\drivers\etc
hosts 파일 열기
```
# Copyright (c) 1993-2009 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
#
# This file contains the mappings of IP addresses to host names. Each
# entry should be kept on an individual line. The IP address should
# be placed in the first column followed by the corresponding host name.
# The IP address and the host name should be separated by at least one
# space.
#
# Additionally, comments (such as these) may be inserted on individual
# lines or following the machine name denoted by a '#' symbol.
#
# For example:
#
#      102.54.94.97     rhino.acme.com          # source server
#       38.25.63.10     x.acme.com              # x client host

# localhost name resolution is handled within DNS itself.
#	127.0.0.1       localhost
#	::1             localhost

172.16.8.30 example.com
```
이렇게 아래에 172.16.8.30 example.com
추가


이러면 브라우저에서 example.com 으로 인덱스페이지를 열 수 있다
