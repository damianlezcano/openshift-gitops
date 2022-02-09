# Instalamos Openshift gitops desde el operador

El operador crea un namespace `openshift-gitops` y dentro un CR `openshift-gitops` (hay que esperar..)

Hay que crear un `rbac` con los permisos para que ArgoCD pueda generar namespace.

```bash
oc create -f ocp02/proyectos/openshift-gitops/rolebinding.yaml
```

# Agregamos repo 'openshift-gitops' y secret con las credenciales de acceso

oc create -f ocp02/core/apps-repository.yaml
oc create -f ocp02/core/github-ssh-repo-creds.yaml

# Agregamos repo 'reprocann-dev'

oc create -f ocp02/repositories/reprocann-apps-repository.yaml


# Agregamos proyecto y aplicacion argocd

oc create -f ocp02/core/openshift-gitops-project.yaml
oc create -f ocp02/core/applications.yaml


# Creamos la imagen de la aplicacion de prueba

```bash
oc new-build openshift/python:3.8-ubi8~https://github.com/elsony/devfile-sample-python-basic.git -n openshift
```

