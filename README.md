# My container toolbox based on [ubi8](https://catalog.redhat.com/software/container-stacks/detail/5ec53f50ef29fd35586d9a56) [![Docker Repository on Quay](https://quay.io/repository/openshift-examples/toolbox/status "Docker Repository on Quay")](https://quay.io/repository/openshift-examples/toolbox)

## Installed tools

 * grpcurl v1.7.0
 * latest oc & kubectl
 * latest helm
 * jq 1.6
 * yq 3.4.1

## Ready to use on [quay.io](https://quay.io/repository/openshift-examples/toolbox)

https://quay.io/repository/openshift-examples/toolbox

## Run on OpenShift/Kubernetes
```
oc apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: toolbox
spec:
  containers:
    - name: toolsbox
      image: quay.io/openshift-examples/toolbox:latest
  restartPolicy: Never
EOF
```

## Build & Run via podman

## Build & Run via docker
```
git clone https://github.com/openshift-examples/toolbox.git
cd toolbox
docker build -t toolbox -f Containerfile .
docker run -ti toolbox bash
```

# Example

## dns-checker

```bash
oc new-project dns-checker
oc adm policy add-cluster-role-to-user cluster-reader -z default
oc apply -f https://raw.githubusercontent.com/openshift-examples/toolbox/main/dns-checker.daemonset.yaml

```

Example logout:
```
# Collected DNS Endpoints: 10.129.0.40 10.129.2.5 10.130.0.13 10.130.2.3 10.131.0.7 10.131.2.3
# Run on Node: compute-1.ocp3.stormshift.coe.muc.redhat.com
# Fri Jan  8 13:04:32 UTC 2021
DNS IP: 10.129.0.40      : PASS      (Details: 172.30.0.1 from server 10.129.0.40 in 0 ms. )
DNS IP: 10.129.2.5       : PASS      (Details: 172.30.0.1 from server 10.129.2.5 in 0 ms. )
DNS IP: 10.130.0.13      : PASS      (Details: 172.30.0.1 from server 10.130.0.13 in 3 ms. )
DNS IP: 10.130.2.3       : PASS      (Details: 172.30.0.1 from server 10.130.2.3 in 1 ms. )
DNS IP: 10.131.0.7       : PASS      (Details: 172.30.0.1 from server 10.131.0.7 in 0 ms. )
DNS IP: 10.131.2.3       : PASS      (Details: 172.30.0.1 from server 10.131.2.3 in 0 ms. )
```