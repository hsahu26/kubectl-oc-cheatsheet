 How to know specific configmap is being used by how many deployment config ( it will check two settings to know whether configmap is being used or not for specific dc which are volumes and envFrom option)

    $ oc get dc  -n demo -o json | jq -r '.items | map(select(.spec.template.spec.containers[]?.envFrom[]?.configMapRef.name == "demo1-service-configmap" ) | .metadata.name) | .[]' && \ 
    oc get dc -n demo -o json | jq -r '.items | map(select(.spec.template.spec.volumes[]?.configMap.name == "demo1-service-configmap" ) | .metadata.name) | .[]' | uniq
