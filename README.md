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

