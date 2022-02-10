# Instalamos Openshift gitops desde el operador

El operador crea un namespace `openshift-gitops` y dentro un CR `openshift-gitops` (hay que esperar..)

Hay que crear un `rbac` con los permisos para que ArgoCD pueda generar namespace.

```sh
oc create -f ocp02/proyectos/openshift-gitops/rolebinding.yaml
```

# Registramos repositorio 'openshift-gitops' y secret con las credenciales de acceso

```sh
oc create -f ocp02/core/apps-repository.yaml
oc create -f ocp02/core/github-ssh-repo-creds.yaml
```

# Registramos aplicacion de prueba

## Creamos la imagen para la aplicacion de prueba

```sh
oc new-build openshift/python:3.8-ubi8~https://github.com/elsony/devfile-sample-python-basic.git -n openshift
```

## Registramos repositorio 'personal-service-dev'

```sh
oc create -f ocp02/repositories/personal-service-apps-repository.yaml
```

## Registramos proyecto y aplicacion en argocd

```sh
oc create -f ocp02/core/openshift-gitops-project.yaml
oc create -f ocp02/core/applications.yaml
```