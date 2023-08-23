1. 安装 podman、kubectl、kind
2. 创建 kind ：kind create cluster --config config.yaml
3. 创建 deployment：kubectl create deployment hello-world-flask --image=lyzhang1999/hello-world-flask:latest --replicas=2
4. 生成 yaml文件：kubectl create deployment hello-world-flask --image lyzhang1999/hello-world-flask:latest --replicas=2 --dry-run=client -o yaml
5. 创建 service：kubectl create service clusterip hello-world-flask --tcp=5000:5000
6. 创建 ingress：kubectl create ingress hello-world-flask --rule="/=hello-world-flask:5000"
7. 创建 ingress-nginx：kubectl create -f https://ghproxy.com/https://raw.githubusercontent.com/lyzhang1999/resource/main/ingress-nginx/ingress-nginx.yaml
8. 访问测试：while true; do sleep 1; curl http://127.0.0.1; echo -e '\n'$(date);done
9. 模拟宕机：kubectl exec -it hello-world-flask-56fbff68c8-2xz7w -- bash -c "killall python3"
10. 创建 metric server：kubectl apply -f https://ghproxy.com/https://raw.githubusercontent.com/lyzhang1999/resource/main/metrics/metrics.yaml
11. 等待deployment创建成功：kubectl wait deployment -n kube-system metrics-server --for condition=Available=True --timeout=90s
12. 创建自动扩容策略： kubectl autoscale deployment hello-world-flask --cpu-percent=50 --min=2 --max=10
13. deployment 设置资源配额：kubectl patch deployment hello-world-flask --type='json' -p='[{"op": "add", "path": "/spec/template/spec/containers/0/resources", "value": {"requests": {"memory": "100Mi", "cpu": "100m"}}}]'
14. 查看最新创建的pod：kubectl get pod --field-selector=status.phase==Running
15. 创建并发请求：kubectl exec -it hello-world-flask-64dd645c57-4clbp -- ab -c 50 -n 10000 http://127.0.0.1:5000/
16. 查看 pod 数量：k get pods -w
