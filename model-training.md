== Model Traning in OpenShift.

In order for your application to successfully make predictions, it will require a properly trained model. In this section we will be training the model that the application will be using later.

A model is essentially a mathematical function (Think something like y = mx + b). The training process determines the parameters for the function that are needed to get the results we want.

With the help of Tensor Flow, training becomes a pretty straight forward process. We already have tagged data which will tell our model what the expected outcome for the object is. Tensor Flow will handle creating the model from the tagged data. Since we have a limited number of objects to identify, we will only be using a subset of the tagged data for the training so that we have data we can use for testing/verification.

Once we have a trained model, we need to verify that it is able to accurately predict the nature of a new object. The goal is to have a distinct separation on a graph between the different groups of objects.

Now that we have a model that we are satisfied with, we can export the model for use in our application.

