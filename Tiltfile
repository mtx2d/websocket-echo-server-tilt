docker_build('echo-server-image',
    context='./echo-server',
    dockerfile='./echo-server/Dockerfile'
)

k8s_yaml('ingress.yaml')
k8s_yaml('deployment.yaml')
k8s_yaml('service.yaml')

# install the haproxy ingress controller
k8s_yaml('namespace.yaml') # add the haproxy namespace
load('ext://helm_resource', 'helm_resource', 'helm_repo')
helm_repo('haproxytech', 'https://haproxytech.github.io/helm-charts')
helm_resource('haproxy', 
    'haproxytech/kubernetes-ingress', 
    namespace='haproxy-ingress-controller', 
    flags=['--values=./values.yaml']
)

