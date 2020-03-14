
<h2>Install Helm</h2>

https://www.digitalocean.com/community/tutorials/how-to-install-software-on-kubernetes-clusters-with-the-helm-package-manager - 2.X

https://helm.sh/docs/intro/install/ - 3.X


<h2>Migrate from Helm v2 to Helm v3 (if necessary)</h2>

https://helm.sh/blog/migrate-from-helm-v2-to-helm-v3


<h2>Add stable repo for v3:</h2>

`helm repo add stable https://kubernetes-charts.storage.googleapis.com/`


<h2>Install NFS Server via Helm</h2>

https://docs.bitnami.com/tutorials/deploy-applications-nfs-kubernetes/

v2
`helm install --name my-nfs-server stable/nfs-server-provisioner --set persistence.enabled=true,persistence.size=20Gi`

v3
`helm install my-nfs-server stable/nfs-server-provisioner --set persistence.enabled=true,persistence.size=20Gi`


<h3>How To Set Up an Nginx Ingress on DigitalOcean Kubernetes Using Helm (Optional)</h3>

https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nginx-ingress-on-digitalocean-kubernetes-using-helm#step-1-%E2%80%94-setting-up-hello-world-deployments

<h3>How to Set Up an Nginx Ingress with Cert-Manager on DigitalOcean Kubernetes</h3>

https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nginx-ingress-with-cert-manager-on-digitalocean-kubernetes#step-1-%E2%80%94-setting-up-dummy-backend-services


<h2>Create these mandatory resources:</h2>

`kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.24.1/deploy/mandatory.yaml`


<h2>Create the LoadBalancer Service:</h2>

`kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.24.1/deploy/provider/cloud-generic.yaml`



<h2>Create the cert-manager Custom Resource Definitions (CRDs). Create these by applying them directly from the cert-manager GitHub repository :</h2>

<h4>CHECK FOR UPGRADES</h4>
  
https://cert-manager.io/docs/installation/upgrading/

`kubectl apply -f https://raw.githubusercontent.com/jetstack/cert-manager/release-0.13/deploy/manifests/00-crds.yaml`

<h2>Next, we’ll add a label to the kube-system namespace, where we’ll install cert-manager, to enable advanced resource validation using a webhook:</h2>

`kubectl label namespace kube-system certmanager.k8s.io/disable-validation="true"`

<h2>Now, we’ll add the Jetstack Helm repository to Helm. This repository contains the cert-manager Helm chart.</h2>

`helm repo add jetstack https://charts.jetstack.io`

<h2>Finally, we can install the chart into the kube-system namespace:</h2>

v2
`helm install --name cert-manager --namespace kube-system jetstack/cert-manager --version v0.13.0`

v3
`helm install cert-manager --namespace kube-system jetstack/cert-manager --version v0.13.0`
`helm upgrade cert-manager --namespace kube-system jetstack/cert-manager --version v0.13.1`



<h2>Create Prod Certificate Issuer</h2>

`kubectl apply -f prod_issuer.yaml`


<h2>Install Wordpress</h2>

`kubectl create secret generic mysql --from-literal=password=SOME-SECRET-PASSWORD`

`kubectl apply -f ./k8s-wordpress/`


<h2>Install Linkerd</h2>

https://linkerd.io/2/getting-started/




