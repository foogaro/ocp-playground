# OpenShift Container Platform playground
Here are my experiments with OpenShift (also OCP).
They are about Cloud Native Application, Microservices, BlueGreen deployment, A/B Testing, Canary release, Service Mesh, Pipelines and hopefully more.

# OCP installation
## Prerequisite
For the purpose of this playground, I'm going to use ```oc cluster up``` as OpenShift installation.
You will mainly need two pieces of software:
* Docker
* OpenShift (Origin) client tool

### Docker
By now, I really do think that you should be able to install it yourself!
Go get it.

By the way, here is my ```docker version``` I am using:
```bash
[luigi@foogaro ocp-playground]$ docker version
Client:
 Version:         1.13.1
 API version:     1.26
 Package version: docker-1.13.1-59.gitaf6b32b.fc27.x86_64
 Go version:      go1.9.6
 Git commit:      30c1ca9-unsupported
 Built:           Tue Jun 12 19:29:50 2018
 OS/Arch:         linux/amd64

Server:
 Version:         1.13.1
 API version:     1.26 (minimum version 1.12)
 Package version: docker-1.13.1-59.gitaf6b32b.fc27.x86_64
 Go version:      go1.9.6
 Git commit:      30c1ca9-unsupported
 Built:           Tue Jun 12 19:29:50 2018
 OS/Arch:         linux/amd64
 Experimental:    false
```

### OC client tool
The "oc" binary can be downloaded from the Red Hat Cutomer Portal (need subscription though) at the following URL:
* https://access.redhat.com/downloads/content/290

Alternatively, you can download the community version from the following site:
* https://github.com/openshift/origin/releases

By the way, here is my ```oc version``` I am using:
```bash
[luigi@foogaro ocp-playground]$ oc version
oc v3.10.14
kubernetes v1.10.0+b81c8f8
features: Basic-Auth GSSAPI Kerberos SPNEGO
```
## Installation
The installation is pretty easy, and it consist of launching the OCP cluster itself with the following command:
```bash
[luigi@foogaro ocp-playground]$ oc cluster up --base-dir="existing-config" 
```
Where ```$ocp_home``` is equal to "existing-config".

The first time you run the cluster it will puul all Docker images, and it will instantiate the needed containers, as shown below:
```bash
[luigi@foogaro ocp-playground]$ oc cluster up --base-dir="existing-config" 
OCP Home existing-config
Getting a Docker client ...
Checking if image registry.access.redhat.com/openshift3/ose-control-plane:v3.10 is available ...
Pulling image registry.access.redhat.com/openshift3/ose-control-plane:v3.10
Pulled 2/4 layers, 51% complete
Pulled 3/4 layers, 76% complete
Pulled 3/4 layers, 82% complete
Pulled 3/4 layers, 89% complete
Pulled 3/4 layers, 94% complete
Pulled 4/4 layers, 100% complete
Extracting
Image pull complete
Pulling image registry.access.redhat.com/openshift3/ose-cli:v3.10
Pulled 3/4 layers, 78% complete
Pulled 4/4 layers, 100% complete
Extracting
Image pull complete
Pulling image registry.access.redhat.com/openshift3/ose-node:v3.10
Pulled 4/5 layers, 81% complete
Pulled 4/5 layers, 85% complete
Pulled 4/5 layers, 92% complete
Pulled 4/5 layers, 96% complete
Pulled 5/5 layers, 100% complete
Extracting
Image pull complete
Checking type of volume mount ...
Determining server IP ...
Checking if OpenShift is already running ...
Checking for supported Docker version (=>1.22) ...
Checking if insecured registry is configured properly in Docker ...
Checking if required ports are available ...
Checking if OpenShift client is configured properly ...
Checking if image registry.access.redhat.com/openshift3/ose-control-plane:v3.10 is available ...
Starting OpenShift using registry.access.redhat.com/openshift3/ose-control-plane:v3.10 ...
I0810 13:02:22.697225    3667 config.go:42] Running "create-master-config"
I0810 13:02:25.170528    3667 config.go:46] Running "create-node-config"
I0810 13:02:25.949949    3667 flags.go:30] Running "create-kubelet-flags"
I0810 13:02:26.641361    3667 run_kubelet.go:48] Running "start-kubelet"
I0810 13:02:26.930101    3667 run_self_hosted.go:172] Waiting for the kube-apiserver to be ready ...
I0810 13:05:03.949261    3667 interface.go:26] Installing "kube-proxy" ...
I0810 13:05:03.949322    3667 interface.go:26] Installing "kube-dns" ...
I0810 13:05:03.949343    3667 interface.go:26] Installing "openshift-apiserver" ...
I0810 13:05:03.949403    3667 apply_template.go:83] Installing "openshift-apiserver"
I0810 13:05:03.949946    3667 apply_template.go:83] Installing "kube-proxy"
I0810 13:05:03.950645    3667 apply_template.go:83] Installing "kube-dns"
I0810 13:05:06.010164    3667 interface.go:41] Finished installing "kube-proxy" "kube-dns" "openshift-apiserver"
I0810 13:05:59.032697    3667 run_self_hosted.go:224] openshift-apiserver available
I0810 13:05:59.032728    3667 interface.go:26] Installing "openshift-controller-manager" ...
I0810 13:05:59.032766    3667 apply_template.go:83] Installing "openshift-controller-manager"
I0810 13:06:00.908586    3667 interface.go:41] Finished installing "openshift-controller-manager"
Adding default OAuthClient redirect URIs ...
Adding rhel-imagestreams ...
Adding persistent-volumes ...
Adding web-console ...
Adding registry ...
Adding router ...
Adding sample-templates ...
I0810 13:06:00.943445    3667 interface.go:26] Installing "rhel-imagestreams" ...
I0810 13:06:00.943461    3667 interface.go:26] Installing "persistent-volumes" ...
I0810 13:06:00.943483    3667 interface.go:26] Installing "openshift-web-console-operator" ...
I0810 13:06:00.943495    3667 interface.go:26] Installing "openshift-image-registry" ...
I0810 13:06:00.943507    3667 interface.go:26] Installing "openshift-router" ...
I0810 13:06:00.943517    3667 interface.go:26] Installing "sample-templates" ...
I0810 13:06:00.943571    3667 interface.go:26] Installing "sample-templates/mysql" ...
I0810 13:06:00.943583    3667 interface.go:26] Installing "sample-templates/rails quickstart" ...
I0810 13:06:00.943595    3667 interface.go:26] Installing "sample-templates/jenkins pipeline ephemeral" ...
I0810 13:06:00.943606    3667 interface.go:26] Installing "sample-templates/mongodb" ...
I0810 13:06:00.943617    3667 interface.go:26] Installing "sample-templates/mariadb" ...
I0810 13:06:00.943636    3667 interface.go:26] Installing "sample-templates/postgresql" ...
I0810 13:06:00.943648    3667 interface.go:26] Installing "sample-templates/cakephp quickstart" ...
I0810 13:06:00.943661    3667 interface.go:26] Installing "sample-templates/dancer quickstart" ...
I0810 13:06:00.943673    3667 interface.go:26] Installing "sample-templates/django quickstart" ...
I0810 13:06:00.943684    3667 interface.go:26] Installing "sample-templates/nodejs quickstart" ...
I0810 13:06:00.943704    3667 interface.go:26] Installing "sample-templates/sample pipeline" ...
I0810 13:06:00.943782    3667 apply_list.go:68] Installing "sample-templates/sample pipeline"
I0810 13:06:00.944034    3667 apply_list.go:68] Installing "sample-templates/jenkins pipeline ephemeral"
I0810 13:06:00.944061    3667 apply_list.go:68] Installing "rhel-imagestreams"
I0810 13:06:00.944681    3667 apply_list.go:68] Installing "sample-templates/mysql"
I0810 13:06:00.945051    3667 apply_list.go:68] Installing "sample-templates/rails quickstart"
I0810 13:06:00.945408    3667 apply_list.go:68] Installing "sample-templates/mariadb"
I0810 13:06:00.945516    3667 apply_template.go:83] Installing "openshift-web-console-operator"
I0810 13:06:00.945620    3667 apply_list.go:68] Installing "sample-templates/mongodb"
I0810 13:06:00.945831    3667 apply_list.go:68] Installing "sample-templates/django quickstart"
I0810 13:06:00.945902    3667 apply_list.go:68] Installing "sample-templates/dancer quickstart"
I0810 13:06:00.946050    3667 apply_list.go:68] Installing "sample-templates/postgresql"
I0810 13:06:00.946136    3667 apply_list.go:68] Installing "sample-templates/nodejs quickstart"
I0810 13:06:00.946261    3667 apply_list.go:68] Installing "sample-templates/cakephp quickstart"
I0810 13:06:09.254166    3667 interface.go:41] Finished installing "sample-templates/mysql" "sample-templates/rails quickstart" "sample-templates/jenkins pipeline ephemeral" "sample-templates/mongodb" "sample-templates/mariadb" "sample-templates/postgresql" "sample-templates/cakephp quickstart" "sample-templates/dancer quickstart" "sample-templates/django quickstart" "sample-templates/nodejs quickstart" "sample-templates/sample pipeline"
I0810 13:07:08.690270    3667 interface.go:41] Finished installing "rhel-imagestreams" "persistent-volumes" "openshift-web-console-operator" "openshift-image-registry" "openshift-router" "sample-templates"
Login to server ...
Creating initial project "myproject" ...
Server Information ...
OpenShift server started.

The server is accessible via web console at:
    https://127.0.0.1:8443

You are logged in as:
    User:     developer
    Password: <any value>

To login as administrator:
    oc login -u system:admin

```
In your OCP home you will find the following folders containing metatdata and status of the cluster:
```bash
[luigi@foogaro ocp-playground]$ ls -lrt existing-config/
total 80
drwxr-xr-x.   2 luigi luigi 4096 Aug 10 13:02 openshift-apiserver
drwxr-xr-x.   2 luigi luigi 4096 Aug 10 13:02 openshift-controller-manager
drwx------.   2 luigi luigi 4096 Aug 10 13:02 node
drwx------.   2 luigi luigi 4096 Aug 10 13:02 kubedns
drwxr-xr-x.   2 luigi luigi 4096 Aug 10 13:02 static-pod-manifests
drwxr-xr-x.   5 luigi luigi 4096 Aug 10 13:02 openshift.local.volumes
drwxr-xr-x.   3 luigi luigi 4096 Aug 10 13:04 etcd
drwxr-xr-x.   2 luigi luigi 4096 Aug 10 13:06 kube-apiserver
drwxr-xr-x.   2 luigi luigi 4096 Aug 10 13:06 logs
drwxr-xr-x. 103 luigi luigi 4096 Aug 10 13:06 openshift.local.pv
```

To stop the OpenShift cluster, just invoke the following commad:
```bash
[luigi@foogaro ocp-playground]$ oc cluster down
```
The next time the ```oc cluster up``` command will provide the following output:
```bash
[luigi@foogaro ocp-playground]$ oc cluster up --base-dir="existing-config" 
OCP Home existing-config
Getting a Docker client ...
Checking if image registry.access.redhat.com/openshift3/ose-control-plane:v3.10 is available ...
Checking type of volume mount ...
Determining server IP ...
Checking if OpenShift is already running ...
Checking for supported Docker version (=>1.22) ...
Checking if insecured registry is configured properly in Docker ...
Checking if required ports are available ...
Checking if OpenShift client is configured properly ...
Checking if image registry.access.redhat.com/openshift3/ose-control-plane:v3.10 is available ...
Starting OpenShift using registry.access.redhat.com/openshift3/ose-control-plane:v3.10 ...
I0810 13:16:42.889242   26031 flags.go:30] Running "create-kubelet-flags"
I0810 13:16:43.500209   26031 run_kubelet.go:48] Running "start-kubelet"
I0810 13:16:43.912920   26031 run_self_hosted.go:172] Waiting for the kube-apiserver to be ready ...
I0810 13:17:32.934500   26031 interface.go:26] Installing "kube-proxy" ...
I0810 13:17:32.934528   26031 interface.go:26] Installing "kube-dns" ...
I0810 13:17:32.934542   26031 interface.go:26] Installing "openshift-apiserver" ...
I0810 13:17:32.934580   26031 apply_template.go:83] Installing "openshift-apiserver"
I0810 13:17:32.934838   26031 apply_template.go:83] Installing "kube-proxy"
I0810 13:17:32.935033   26031 apply_template.go:83] Installing "kube-dns"
I0810 13:17:35.837069   26031 interface.go:41] Finished installing "kube-proxy" "kube-dns" "openshift-apiserver"
I0810 13:18:04.864957   26031 run_self_hosted.go:224] openshift-apiserver available
I0810 13:18:04.864996   26031 interface.go:26] Installing "openshift-controller-manager" ...
I0810 13:18:04.865021   26031 apply_template.go:83] Installing "openshift-controller-manager"
I0810 13:18:07.040469   26031 interface.go:41] Finished installing "openshift-controller-manager"
Adding default OAuthClient redirect URIs ...
Adding persistent-volumes ...
Adding registry ...
Adding rhel-imagestreams ...
Adding router ...
Adding sample-templates ...
Adding web-console ...
I0810 13:18:07.065525   26031 interface.go:26] Installing "persistent-volumes" ...
I0810 13:18:07.065544   26031 interface.go:26] Installing "openshift-image-registry" ...
I0810 13:18:07.065557   26031 interface.go:26] Installing "rhel-imagestreams" ...
I0810 13:18:07.065567   26031 interface.go:26] Installing "openshift-router" ...
I0810 13:18:07.065575   26031 interface.go:26] Installing "sample-templates" ...
I0810 13:18:07.065585   26031 interface.go:26] Installing "openshift-web-console-operator" ...
I0810 13:18:07.065872   26031 interface.go:26] Installing "sample-templates/nodejs quickstart" ...
I0810 13:18:07.069350   26031 interface.go:26] Installing "sample-templates/jenkins pipeline ephemeral" ...
I0810 13:18:07.069370   26031 interface.go:26] Installing "sample-templates/postgresql" ...
I0810 13:18:07.069380   26031 interface.go:26] Installing "sample-templates/cakephp quickstart" ...
I0810 13:18:07.069389   26031 interface.go:26] Installing "sample-templates/django quickstart" ...
I0810 13:18:07.069409   26031 interface.go:26] Installing "sample-templates/dancer quickstart" ...
I0810 13:18:07.069425   26031 interface.go:26] Installing "sample-templates/rails quickstart" ...
I0810 13:18:07.069441   26031 interface.go:26] Installing "sample-templates/sample pipeline" ...
I0810 13:18:07.069458   26031 interface.go:26] Installing "sample-templates/mongodb" ...
I0810 13:18:07.069477   26031 interface.go:26] Installing "sample-templates/mariadb" ...
I0810 13:18:07.069500   26031 interface.go:26] Installing "sample-templates/mysql" ...
I0810 13:18:07.069583   26031 apply_list.go:68] Installing "sample-templates/mysql"
I0810 13:18:07.066245   26031 apply_template.go:83] Installing "openshift-web-console-operator"
I0810 13:18:07.070121   26031 apply_list.go:68] Installing "sample-templates/nodejs quickstart"
I0810 13:18:07.070347   26031 apply_list.go:68] Installing "sample-templates/jenkins pipeline ephemeral"
I0810 13:18:07.070567   26031 apply_list.go:68] Installing "sample-templates/postgresql"
I0810 13:18:07.070785   26031 apply_list.go:68] Installing "sample-templates/cakephp quickstart"
I0810 13:18:07.070989   26031 apply_list.go:68] Installing "sample-templates/django quickstart"
I0810 13:18:07.071183   26031 apply_list.go:68] Installing "sample-templates/dancer quickstart"
I0810 13:18:07.071490   26031 apply_list.go:68] Installing "sample-templates/rails quickstart"
I0810 13:18:07.071946   26031 apply_list.go:68] Installing "sample-templates/sample pipeline"
I0810 13:18:07.072830   26031 apply_list.go:68] Installing "sample-templates/mongodb"
I0810 13:18:07.072961   26031 apply_list.go:68] Installing "sample-templates/mariadb"
I0810 13:18:07.067252   26031 apply_list.go:68] Installing "rhel-imagestreams"
I0810 13:18:13.758108   26031 interface.go:41] Finished installing "sample-templates/nodejs quickstart" "sample-templates/jenkins pipeline ephemeral" "sample-templates/postgresql" "sample-templates/cakephp quickstart" "sample-templates/django quickstart" "sample-templates/dancer quickstart" "sample-templates/rails quickstart" "sample-templates/sample pipeline" "sample-templates/mongodb" "sample-templates/mariadb" "sample-templates/mysql"
I0810 13:18:14.439438   26031 interface.go:41] Finished installing "persistent-volumes" "openshift-image-registry" "rhel-imagestreams" "openshift-router" "sample-templates" "openshift-web-console-operator"
Server Information ...
OpenShift server started.

The server is accessible via web console at:
    https://127.0.0.1:8443

```
It will still take a couple of minutes to run a real OpenShift cluster based entirely on Docker.

## Web Console
Now you can login as a "developer", with username "developer" and any password.
Once it here is how OpenShift will look like:

![alt text][web-console]


[web-console]: https://github.com/foogaro/ocp-playground/blob/v3.10/web-console-01.png "OpenShift Container Platform"
