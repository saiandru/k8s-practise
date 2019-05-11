This Repository helps you understand how to deploy Tomcat and Mongo on K8 Standalone cluster.
Note: VM workstation.
      Cloud Providers(not done)
Standalone cluster = Using kubeadm on single node and configuring all so we are using here minikube 

1.For Debain/Redhat: 
Please Follow below sequence steps to successfully install minikube:

 At first need to install kubectl :
  https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-on-linux
  Follow above link you find your required os installation steps

 To check successful installation :
   ]$ sudo kubectl get version : If you get client and version output kubectl configured properly 

 Now Minikube installation procedure:
   https://kubernetes.io/docs/tasks/tools/install-minikube/#install-minikube
   Follow above link and install the minkube on server.
 To check successful installation:
   ]$ sudo minikube version 
   ]$ sudo kubectl version 

2. Create Dashboard of K8:
   ]$ sudo minikube dashboard
   ]$ sudo kubectl proxy

   Please edit the below 
   ]$ sudo kubectl -n kube-system edit service kubernetes-dashboard 
   Above change clusterip to nodeport to access it from outside of your VM

   ]$ sudo kubectl get services --all-namespaces 
   Above gives the port which the dashboard is running on. 

   ]$ sudo minikube service list
   Gives you all services which can be accessed externally.

3. Deployment of Tomcat and running:
  ]$ sudo kubectl create -f tomcatdeployment.yml
  Above command deploys tomcat pods based on your required no of replicas

  ]$ sudo kubectl expose deployment tomcat-deployment --type=NodePort --port=8080
  Above command creates a service and to check type below command
  ]$ sudo kubectl get services 

  In above type we used Nodeport : we use this to access the pods outside cluster Ip
  For Adding to cloud and accessing it to publicly use load balance kind.
  ]$ sudo minikube service list
   Gives you all services which can be accessed externally.

4. Deployment of Mongo and running:
   ]$ sudo kubectl create -f monogdeployment.yml
   ]$ sudo kubectl expose deployment mongo-deployment --type=Nodeport --port=27017
  The above two creates a pod and service for that you can access mongodb and deploy the files accordingly. 
  

   