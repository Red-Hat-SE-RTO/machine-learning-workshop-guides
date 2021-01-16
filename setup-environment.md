## Setup  Environment via CodeReady Workspaces

**Login to the OpenShift Console [CodeReady Workspaces]({{ ECLIPSE_CHE_URL}}){:target="_blank"}.**  
*Use the following username and password*

* username: {{OPENSHIFT_USER_NAME}}  
* password: {{CHE_USER_PASSWORD}}  
 
 **Click on *Git Clone* in your CodeReady Workspace**
 ```
 {{GIT_URL}}
 ```
 
**Click on  *New terminal***  
![new_terminal.png]({% image_path new_terminal.png %})

**Click on  *Login to OpenShift***  
![new_terminal.png]({% image_path new_terminal.png %})

*Use the following username and password*  

* username: {{OPENSHIFT_USER_NAME}}  
* password: {{OPENSHIFT_USER_PASSWORD}}  


**List your projects.**  
```
oc projects
```

**Switch to notebook.**  
```
oc project userXX-notebooks
```

