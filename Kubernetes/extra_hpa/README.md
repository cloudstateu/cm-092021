<img src="../../../img/logo.png" alt="Chmurowisko logo" width="200" align="right">
<br><br>
<br><br>
<br><br>

# AKS and Azure Key Vault

## LAB Overview

In this lab you are going to create a simple deployment, add a Horizontal Pod Autoscaler that will scale up number of replicas when CPU usage gets high.

---

## Exercise steps

1. Create deployment from a file [`01_deployment.yaml`](./files/01_deployment.yaml)

    ```bash
    kubectl apply -f 01_deployment.yaml
    ```

1. In a new / different window we set the preview in continuous mode of changes in POD:

    ```bash
    kubectl get pods -w
    ```

1. Create a HPA for our deployment:

    ```bash
    kubectl autoscale deployment web --min=1  --max=4 --cpu-percent=30
    ```

1. Log into the web Deployment pod and artificially simulate CPU load

    ```bash
    kubectl exec -it <POD_NAME> -- sh
    ```

1. While logged into the Pod update packages and install `stress` package

    ```bash
    apt-get update
    ```

    ```bash
    apt-get install stress
    ```

1. Start load generation

    ```bash
    stress -c 5
    ```

1. In a new terminal window or tab start watching state of Horizontal Pod Autoscaler

    ```bash
    kubectl get hpa -w
    ```

## END LAB

<br><br>

<center><p>&copy; 2019 Chmurowisko Sp. z o.o.<p></center>
