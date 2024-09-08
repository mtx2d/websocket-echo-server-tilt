docker_build('echo-server-image',
    context='./echo-server',
    dockerfile='./echo-server/Dockerfile'
)

k8s_yaml('ingress.yaml')
k8s_yaml('deployment.yaml')
k8s_yaml('service.yaml')
k8s_yaml('namespace.yaml') # add the haproxy namespace

# install the haproxy ingress controller
load('ext://helm_resource', 'helm_resource', 'helm_repo')
helm_repo('haproxytech', 'https://haproxytech.github.io/helm-charts')
helm_resource('haproxy', 'haproxytech/kubernetes-ingress', namespace='haproxy-ingress-controller', flags=['--values=./values.yaml'])

# haproxy_helm_yaml = helm(
#   './helm/Chart.yaml',
#   # The release name, equivalent to helm --name
#   name='haproxy-kubernetes-ingress',
#   # The namespace to install in, equivalent to helm --namespace
#   namespace='haproxy-controller',
#   # The values file to substitute into the chart.
#   values=['./values.yaml'],
#   # Values to set from the command-line
#   # set=['service.port=1234', 'ingress.enabled=true']
# )

# k8s_yaml(haproxy_helm_yaml)
