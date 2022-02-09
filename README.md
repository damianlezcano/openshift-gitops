# Instalamos Openshift gitops desde el operador

# Agregamos repo con el secret con la anotacion para que argo lo reconosca

apps-repository.yaml

```bash
oc create -f <(echo '
apiVersion: v1
kind: Secret
metadata:
  name: repository-gitops
  namespace: openshift-gitops
  labels:
    argocd.argoproj.io/secret-type: repository
stringData:
  name: GitOps
  url: git@github.com/openshift-gitops.git
  type: git
  insecure: 'true'
')
```

spec:
  rbac:
    policy: |
      p, role:readonly, applications, get, */*, allow
      p, role:readonly, certificates, get, *, allow
      p, role:readonly, clusters, get, *, allow
      p, role:readonly, repositories, get, *, allow
      p, role:readonly, projects, get, *, allow
      p, role:readonly, accounts, get, *, allow
      p, role:readonly, gpgkeys, get, *, allow
      p, role:admin, applications, create, */*, allow
      p, role:admin, applications, update, */*, allow
      p, role:admin, applications, delete, */*, allow
      p, role:admin, applications, sync, */*, allow
      p, role:admin, applications, override, */*, allow
      p, role:admin, applications, action/*, */*, allow
      p, role:admin, certificates, create, *, allow
      p, role:admin, certificates, update, *, allow
      p, role:admin, certificates, delete, *, allow
      p, role:admin, clusters, create, *, allow
      p, role:admin, clusters, update, *, allow
      p, role:admin, clusters, delete, *, allow
      p, role:admin, repositories, create, *, allow
      p, role:admin, repositories, update, *, allow
      p, role:admin, repositories, delete, *, allow
      p, role:admin, projects, create, *, allow
      p, role:admin, projects, update, *, allow
      p, role:admin, projects, delete, *, allow
      p, role:admin, accounts, update, *, allow
      p, role:admin, gpgkeys, create, *, allow
      p, role:admin, gpgkeys, delete, *, allow
      g, role:admin, role:readonly
      g, i8software:Admins, role:admin
      g, system:cluster-admins, role:admin