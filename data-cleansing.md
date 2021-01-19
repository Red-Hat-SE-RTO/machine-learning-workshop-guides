## Data Cleansing in OpenShift.

In this workshop, we'll be learning how to perform basic Data Science and Machine Learning using OpenShift. The OpenShift platform greatly simplifies deploying and using the tools that are typically used in most Data Science workflows today. In particular, we'll be using the [Open Data Hub](http://opendatahub.io) project to deploy most of the infrastructure we'll be using in the lab today.

### Introduction to Open Data Hub

Open Data Hub (ODH) is an open source project based on [Kubeflow](https://kubeflow.org/) that provides open source AI tools for running large and distributed AI workloads on OpenShift Container Platform. Currently, the Open Data Hub project provides open source tools for data storage, distributed AI and Machine Learning (ML) workflows, Jupyter Notebook development environment and monitoring. The Open Data Hub project roadmap offers a view on new tools and integration the project developers are planning to add.

Open Data Hub includes several open source components, which can be individially enabled. They include:

* Apache Airflow
* Apache Kafka
* Apache Spark
* Apache Superset
* Argo
* Grafana
* JupyterHub
* Prometheus
* Seldon

Open Data Hub itself is deployed on OpenShift via an [Operator](https://www.openshift.com/learn/topics/operators). Operators on OpenShift are responsible for managing [Custom Resources](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/). Custom resources allow for OpenShift users to create higher level objects in Kubernetes than are available via the basic Kubernetes API. For example, the AMQ Streams Operator defines a custom resource called "Kafka", which allows us to create a Kafka cluster. Operators can define more than one Custom Resource - the AMQ Streams Operator also allows for the creation of a "KafkaTopic" on our "Kafka" cluster.

### Data Cleansing

The first step in developing a model for machine learning is often cleansing the data on which we're going to operate. In this section of the workshop, we'll learn how to perform basic data cleansing using a set of data available on the Internet. We'll download the data in CSV format and use the Python [Pandas](https://pandas.pydata.org/) library to clean and visualize the data inside of a Jupyter notebook.

[Jupyter notebooks](https://jupyter.org/) are widely used throughout the data science community to organize, run, and share code. Jupyter supports many programming languages, but the most common languages used in data science are Python and R. This workshop's examples will all be in Python, as will the code we use to train and run our model.

In this first exercise, we'll be deploying a Jupyter Hub instance for our user on OpenShift and loading a notebook that performs some basic data cleansing and visualization exercizes on COVID-19 data from the [COVID Tracking project](https://covidtracking.com/).

Start by logging into the [OpenShift web console]({{ CONSOLE_URL}}){:target="_blank"}.

![openshift_login]({% image_path openshift_login.png %})

Login using:

* Username: `userXX`
* Password: `r3dh4t1!` 

You will see the OpenShift landing page:

![openshift_landing]({% image_path openshift_landing.png %})

## Open Data Hub deployment

We'll start by deploying an Open Data Hub (ODH) instance. +

Switch to project for the notebooks.

```
oc project userXX-notebooks
```

### Step 2: Deploy ODH

Change your directory to where the installation files are:

```
cd ocp-machine-learning-workshop
```

Take a look at the ODH deployment file:

```
01_odh.yaml
```

Patch the deployment jupyterhub-db so the deployment may complete.

```
oc patch  dc jupyterhub-db -n userXX-notebooks  --type='json' -p='[{"op": "add", "path": "/spec/template/spec/serviceAccount", "value": "postgres" },{"op": "add", "path": "/spec/template/spec/serviceAccountName", "value": "postgres" }]'
```

You will see from the *spec* section that it will deploy 3 components:

* Some common files
* JupyterHub, which will act as a "launcher" for notebook environments.
* Notebooks images

Let's deploy it!

```
oc apply -f 01_odh.yaml
```

Watch the topology view to see that the jupyterhub and jupyterhub-db deployments succeed. The circles should turn dark blue!

![jupyterhub.png]({% image_path jupyterhub.png %})

## Bucket Storage Access
Your JupyterHub Notebook  requires an `access_key` and `secret_key` that is found in your openshift project as a secret. The Notebook uses this information to storage data and content that you will during this lab. 

You may access this in the terminal by running the commands below. 
* list your secrets you should see a secert called `my-storage-keys`.

```
oc get secrets -n userXX-notebooks
```

* Obtain yur access key from secret. 

```
oc get secrets -n userXX-notebooks my-storage-keys -o jsonpath='{.data.accesskeys}' | base64 -d
```

You may access from the UI as seen below. 
*To-Do add UI instructions*


### Connect to JupyterHub

Click on the jupyterhub icon and look for the "Routes" section. Click on the route listed there.

Just click on this link, a new tab will open. Click on the button *Sign in with OpenShift*, and use your OpenTLC credentials to connect.+
On the first connection, OpenShift will ask to authorize the application to access your username just click *Allow selected permissions*.

### Launch Jupyter

On the *Spawner Options* page select the *s2i-minimal-notebook:3.6* image from the first dropdown (this should be the default image), and click *Spawn* at the bottom.

Your Jupyter environment will take 15-20 seconds to launch.

It will display a _File Explore like_ interface. Click on the *xraylab_notebooks.git* folder, then on the *georgia_covidtracking.ipynb* file, which will launch the notebook.

