# Happy Helming!

Helm chart for a quick demo!

Ran this demo on *OSX* with *minikube* running locally.

## Dry run

```bash
helm install helm-demo --dry-run .
```

## {{ vars }}

In the *templates* folder, *.yaml* files pull values from *Chart.yaml* and *values.yaml* files.

*Chart.yaml* has metadata about the chart, such as name, version etc

*values.yaml* exposes configuration that can be changed/set at the time of deployment. Eg, *service.type, image.repository*


## Installing

For this part of the demo, I am going to run an nginx app that will be exposed at NodePort on k8s. 

**Run:**
```bash
helm install helm-demo . --set service.type=NodePort

  export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services helm-demo)
  export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")

In a browser, open http://$NODE_IP:$NODE_PORT
```
You should see blue version of the app running as below

![v1 of myapp](./static/v1blue.png)

## Upgrading

Let's upgrade the app to a newer version (green)

**Run:**
```bash
helm upgrade helm-demo . --set image.repository=heera88/blue-green-app:v2,service.type=NodePort

In a browser, open http://$NODE_IP:$NODE_PORT
```
You should see blue version of the app running as below

![v2 of myapp](./static/v2green.png)

## Packaging

```bash
helm package .
```
*helm-demo-{{ .Chart.version }}.tgz* should get saved to your working directory


## License
[MIT](https://choosealicense.com/licenses/mit/)
