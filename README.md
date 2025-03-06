# Ansible Execution Environment Pipelines
> Monorepo for housing an example execution environment definition and a tekton pipeline to build it.


## Deploy tkn pipeline 🐈
```bash
oc apply -f tekton --recursive
```

## building an ee on OCP 🔨
```bash
APP_NAME=example
cd ${APP_NAME}
ansible-builder create -f execution-environment.yml --output-filename=Dockerfile

oc new-build --binary --name=${APP_NAME} -l app=${APP_NAME} --strategy=docker
oc start-build ${APP_NAME} --from-dir=context --follow --wait 
```
