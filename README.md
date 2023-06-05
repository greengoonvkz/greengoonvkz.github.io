## Gitlab-Runner

#### Install role

###### Creating namespaces before installing role:

`kubectl create namespace dev`

`kubectl create namespace gitlab-runner`

`kubectl create namespace ingress-nginx`

`kubectl create namespace cert-manager`

### Назначаем роль админа кластера аккаунту раннера

`kubectl apply -f ./runner/role.yaml`

### Добавляем секрет для того, чтобы раннер мог пуллить образы в гитлаб

`kubectl apply -f ./runner/registry-pullsecret.yaml.yaml`

### Все до этого момента выполнить руками при развертывании через гитлаб

#### Add runner repo
`helm repo add gitlab http://charts.gitlab.io/`

#### Install runner

```bash
helm install gitlab-runner gitlab/gitlab-runner \
--namespace gitlab-runner --create-namespace \
--set runnerRegistrationToken=$TOKEN \
--set runners.tags="grill1\, qa\, k8" \
--values ./runner/values.yaml
```

#### Remove runner
```bash
helm uninstall -n gitlab-runner gitlab-runner
```
