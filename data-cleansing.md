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

> **NOTE**: Use of self-signed certificates
>
> When you access the OpenShift web console]({{ CONSOLE_URL}}) or other URLs via _HTTPS_ protocol, you will see browser warnings
> like `Your > Connection is not secure` since this workshop uses self-signed certificates (which you should not do in production!).
> For example, if you're using **Chrome**, you will see the following screen.
>
> Click on `Advanced` then, you can access the HTTPS page when you click on `Proceed to...`!!!
>
> ![warning]({% image_path browser_warning.png %})
>
> Other browsers have similar procedures to accept the security exception.

You will see the OpenShift landing page:

![openshift_landing]({% image_path openshift_landing.png %})

