# Instalamos Openshift gitops desde el operador

El operador crea un namespace `openshift-gitops` y dentro un CR `openshift-gitops` (hay que esperar..)

Hay que crear un `rbac` con los permisos para que ArgoCD pueda generar namespace.

```bash
oc create -f ocp02/proyectos/openshift-gitops/rolebinding.yaml
```

# Agregamos repo y el secret con la anotacion para que argocd lo reconozca

oc create -f ocp02/core/apps-repository.yaml
oc create -f ocp02/core/github-ssh-repo-creds.yaml
oc create -f ocp02/core/openshift-gitops-project.yaml
oc create -f ocp02/core/applications.yaml
