# Integrating New Relic with Kubernetes - Lab 3

Welcome! This lab correlates with the _Integrating New Relic with Kubernetes_ talk from Nerd Days 2020. It is the final hands-on lab you'll walk through in your session.

In this lab, you'll:

- Deploy a Flask app in a local Kubernetes cluster
- Integrate New Relic with your cluster **using helm charts**

Enjoy your session!

## Prerequisites

To complete this lab, you need:

- [Docker](https://docs.docker.com/get-docker/)
- [Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/)
- [A New Relic account](https://newrelic.com/signup)
- [Helm](https://github.com/helm/helm#install)

> **Note:** This lab uses Helm 3, if you're working on a project that uses Helm 2, please see [our documentation](https://docs.newrelic.com/docs/integrations/kubernetes-integration/installation/install-kubernetes-integration-using-helm) for relevant instructions.

Once you've installed the prerequisite software, you may begin the lab.

## Start Minikube

Minikube allows you to spin up a local, single-node Kubernetes cluster on your local machine.

Start a local Minikube cluster:

```console
$ minikube start --driver=docker
```

> **Note:** If you're using a different hypervisor, use your [driver](https://kubernetes.io/docs/setup/learning-environment/minikube/#specifying-the-vm-driver) instead of `docker`.

## Use Minikube Docker daemon

Instead of using a Docker registry for your image, you can build your Docker images inside Minikube's daemon. This simplifies some of the process of deploying your application.

First, run `minikube docker-env`, which sets some environment variables:

```console
$ minikube docker-env
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST=<host>
export DOCKER_CERT_PATH=<cert path>
export MINIKUBE_ACTIVE_DOCKERD="minikube"

# To point your shell to minikube's docker-daemon, run:
# eval $(minikube -p minikube docker-env)
```

Second, if you haven't already, execute the last line from the output:

```console
$ eval $(minikube -p minikube docker-env)
```

## Create resources

In this lab, you'll deploy a small web app in Kubernetes. To do so, build the project's Docker image:

```console
$ docker build -t kube-lab-3 .
```

Then, apply the manifests in the `kube-manifests` directory:

```console
$ kubectl create -f kube-manifests
deployment.apps/kube-lab-3 created
service/kube-lab-3 created
```

Finally, check your resources to make sure they exist:

```console
$ kubectl get pods
NAME                          READY   STATUS    RESTARTS   AGE
kube-lab-3-7c86d647dd-wlb9k   1/1     Running   0          7s

$ kubectl get services
NAME         TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
kube-lab-3   LoadBalancer   10.100.204.209   <pending>     5000:31568/TCP   17s
kubernetes   ClusterIP      10.96.0.1        <none>        443/TCP          2m45s
```

## View your application

Notice the `kube-lab-3` load balancer service's pending `EXTERNAL-IP`. You need to expose the LoadBalancer on localhost, using `minikube tunnel` from a different terminal window:

```console
$ minikube tunnel
🏃  Starting tunnel for service kube-lab-3.
```

Now, you should see an `EXTERNAL-IP`:

```console
$ kubectl get services
NAME         TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
kube-lab-3   LoadBalancer   10.99.10.112   127.0.0.1     5000:30300/TCP   15m
kubernetes   ClusterIP      10.96.0.1      <none>        443/TCP          3h44m
```

Visit the service (at port 5000) in your browser:

## Instrument your service

Great! Now you're running an application in Kubernetes. Next, you'll instrument it with New Relic using our [helm chart](https://docs.newrelic.com/docs/integrations/kubernetes-integration/installation/install-kubernetes-integration-using-helm).

First, add the New Relic Helm repository:

```console
$ helm repo add newrelic https://helm-charts.newrelic.com
```

Second, install the `newrelic-infrastructure` chart:

```console
$ helm install newrelic-bundle newrelic/nri-bundle \
    --set global.licenseKey=<YOUR_LICENSE_KEY> \
    --set global.cluster=Kube-Lab-3 \
    --namespace=default \
    --set newrelic-infrastructure.privileged=true \
    --set ksm.enabled=true
```

Don't forget to replace `<YOUR_LICENSE_KEY`> with your actual license key, which you can find at New Relic:

1. [Log in](https://one.newrelic.com/)
2. Navigate to _Account settings_ from your profile at the top right of the screen
3. Your License key is on the right side, under _Account information_

Finally, wait a few minutes and navigate to the [Kubernetes Explorer](https://docs.newrelic.com/docs/integrations/kubernetes-integration/understand-use-data/kubernetes-cluster-explorer):

1. [Log in](https://one.newrelic.com/)
2. Select _Infrastructure_ from the top navigation
3. Select _NR1 Kubernetes cluster explorer_ on the right side of the screen

![Navigate to the Cluster Explorer](static/cluster_explorer_link.png)

Select the _Kube-Lab-3_ cluster:

![Explore Kubernetes](static/cluster_explorer.png)

> **Don't panic!** If you see a message about incomplete data for the cluster, refresh in a few minutes.

## Tear down

You can remove all your resources from this lab by spinning down Minikube:

```console
$ minikube stop
$ minikube delete
```

## Next Steps

Congratulations! You've successfully deployed and instrumented an app in Kubernetes using Helm. If you don't need the flexibility of a manual install, you can also use the automated installer from lab 1! Instead of selecting _Kubernetes m