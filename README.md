# 多节点点部署


## 说明

适用场景：对数据安全要求高的应用，大型应用。

优点：高可用，容灾性强，支持在线扩容，多副本之间实时自动备份，负载均衡, 无需手动配置, 快速伸缩

缺点：需要多台机器。


#### 1. 添加Helm仓库
```bash
helm repo add wukongim https://wukongim.github.io/helm/
```

#### 2. 更新Helm仓库
```bash
helm repo update
```

#### 3. 搜索可用的 Chart
```bash
helm search repo wukongim
```

#### 4. 部署
```bash
helm install wkim wukongim/wukongim -n wukongim --create-namespace --version 0.1.0 --set replicaCount=3
```

#### 5. service LB 部署示例

如果需要使用云厂商的负载均衡，可以通过 `--set` 设置注解或使用 `values.yaml`。

**通过命令行设置 (以阿里云为例)**
```bash
helm install wkim wukongim/wukongim -n wukongim \
  --set service.type=LoadBalancer \
  --set service.annotations."service\.beta\.kubernetes\.io/alicloud-loadbalancer-address-type"=internet \
  --set service.annotations."service\.beta\.kubernetes\.io/alibaba-cloud-loadbalancer-spec"=slb.s1.small
```

#### 6. 查看安装状态
```bash
helm status wkim
```

#### 7. 卸载
```bash
helm uninstall wkim
```
