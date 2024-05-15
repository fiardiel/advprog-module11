# ADVPROG Module 11

1. Compare the application logs before and after you exposed it as a Service. Try to open the app several times while the proxy into the Service is running. What do you see in the logs? Does the number of logs increase each time you open the app?
![ss1](img/ss1.png)
**Answer:**
    The number of logs increase each time I open the app. It increases by 2 since every time I open the app the HTTP get method appears twice in the log. This is due to the first get method is to get the favicon and the second get method is to get the index.html.


2. Notice that there are two versions of kubectl get invocation during this tutorial section. The first does not have any option, while the latter has -n option with value set to kube-system. What is the purpose of the -n option and why did the output not list the pods/services that you explicitly created?
**Answer:**
    The -n option is used to specify the namespace to list the pods/services. The output did not list the pods/services that I explicitly created because the namespace is set to kube-system. The pods/services that I created are in the default namespace.

