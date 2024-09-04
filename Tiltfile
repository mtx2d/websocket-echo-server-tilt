docker_build('echo-server-image',
    context='./echo-server',
    dockerfile='./echo-server/Dockerfile'
)

k8s_yaml('ingress.yaml')
k8s_yaml('deployment.yaml')
k8s_yaml('service.yaml')
# k8s_yaml('nginx-service.yaml')
# k8s_yaml('pod.yaml')
