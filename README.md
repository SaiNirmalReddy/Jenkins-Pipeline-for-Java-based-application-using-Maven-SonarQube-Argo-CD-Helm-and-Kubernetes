# Jenkins-Pipeline-for-Java-based-application-using-Maven-SonarQube-Argo-CD-Helm-and-Kubernetes
Jenkins Pipeline for Java based application using Maven, SonarQube, Argo CD, Helm and Kubernetes


Jenkins Pipeline for Java based application using Maven, SonarQube, Argo CD, Helm and Kubernetes

From <https://github.com/I-am-Gavini/Jenkins-Zero-To-Heroo/tree/main/java-maven-sonar-argocd-helm-k8s> 



Here are the step-by-step details to set up an end-to-end Jenkins pipeline for a Java application using SonarQube, Argo CD, Helm, and Kubernetes:

Prerequisites:

Java application code hosted on a Git repository
Jenkins server
Kubernetes cluster
Helm package manager
Argo CD



Steps:
1. Install the necessary Jenkins plugins:
   1.1 Git plugin
   1.2 Maven Integration plugin
   1.3 Pipeline plugin
   1.4 Kubernetes Continuous Deploy plugin
2. Create a new Jenkins pipeline:
   2.1 In Jenkins, create a new pipeline job and configure it with the Git repository URL for the Java application.
   2.2 Add a Jenkins file to the Git repository to define the pipeline stages.
3. Define the pipeline stages:
    Stage 1: Checkout the source code from Git.
    Stage 2: Build the Java application using Maven.
    Stage 3: Run unit tests using JUnit and Mockito.
    Stage 4: Run SonarQube analysis to check the code quality.
    Stage 5: Package the application into a JAR file.
    Stage 6: Deploy the application to a test environment using Helm.
    Stage 7: Run user acceptance tests on the deployed application.
    Stage 8: Promote the application to a production environment using Argo CD.
4. Configure Jenkins pipeline stages:
    Stage 1: Use the Git plugin to check out the source code from the Git repository.
    Stage 2: Use the Maven Integration plugin to build the Java application.
    Stage 3: Use the JUnit and Mockito plugins to run unit tests.
    Stage 4: Use the SonarQube plugin to analyze the code quality of the Java application.
    Stage 5: Use the Maven Integration plugin to package the application into a JAR file.
    Stage 6: Use the Kubernetes Continuous Deploy plugin to deploy the application to a test environment using Helm.
    Stage 7: Use a testing framework like Selenium to run user acceptance tests on the deployed application.
    Stage 8: Use Argo CD to promote the application to a production environment.
5. Set up Argo CD:
    Install Argo CD on the Kubernetes cluster.
    Set up a Git repository for Argo CD to track the changes in the Helm charts and Kubernetes manifests.
    Create a Helm chart for the Java application that includes the Kubernetes manifests and Helm values.
    Add the Helm chart to the Git repository that Argo CD is tracking.
6. Configure Jenkins pipeline to integrate with Argo CD:
   6.1 Add the Argo CD API token to Jenkins credentials.
   6.2 Update the Jenkins pipeline to include the Argo CD deployment stage.
7. Run the Jenkins pipeline:
   7.1 Trigger the Jenkins pipeline to start the CI/CD process for the Java application.
   7.2 Monitor the pipeline stages and fix any issues that arise.
This end-to-end Jenkins pipeline will automate the entire CI/CD process for a Java application, from code checkout to production deployment, using popular tools like SonarQube, Argo CD, Helm, and Kubernetes.



Interview Questions

1. Git - Jenkins , There is a Git repository and how does changes and modifications are notified by Jenkins and how the Jenkins pipeline is triggered?
Ans : We have something called "webhooks" in Jenkins and this webhook URL is used to configure by putting this URL in Github Settings by that Jenkins will come to know for which action , webhook needs to be triggered like by some actions like "commit,push" . Whenever Developer creates a pull request then "Git" will send the notifications to the Jenkins and ask Jenkins to trigger the pipeline.

Hereafter, Devops Engineer role comes into the picture,

-> For example, you are managing the Jenkins installation and managing the plugins and let's say you are not responsible for all these things , then you will write a "Jenkins file" and then by using the "Jenkins file" , you will perform the set of actions  using your Jenkins files on your Jenkins.

-> Set of actions are like firstly we use "Maven" because you are talking about the Java application and this Maven is used to build the application ,

And how we configure the "Maven" plugin is by , you go to your Jenkins and configure the system and install Maven or the other thing you can do is for each of these stages we can use "Docker as an agent" and when you use the Docker agent , you don't worry about the installations and configurations at all because Docker Images are directly available for these things .

-> Now as part of build what happens " Unit test" will done and later " Static Code Analysis" will be done and if both these things are successful, then only you will move to the next stage .

-> If the build fails , you can configure some alerts like we can send out email notifications by using the Email Plugins in Jenkins .

-> Next , if the build passes then we will move to the next stage and as part of the next stage, you can integrate it with the "SonarQube" or any other code scanning tools -> and it will verify the previous part and if there are any security vulnerabilities , then it will send out the "email notifications" and if there are no security vulnerabilities, then we can proceed with the creation of "Docker Image" -> then after running the commands , you will get a "Docker Image" , then as part of the pipeline , you will these "Docker Image" to a "Docker Registry" and this complete process is said to be "Continuous Integration" . 

-> In a nutshell , what we have done in "Continuous Integration" is Firstly , we have started with "  a Developer is raising a pull request and trying to push the source code into the Git repository" and here "Git can talk to Jenkins by using webhooks" then by using the declarative Jenkins pipelines  by writing the Jenkinsfile and the agents we use "Dockeragent" which is light in weight because we don't have to do some installations and we don't have to install "Maven" or if we are using python, we don't have to install them, because these are present in Dockerfile, and after we use Maven to build the application and if it goes good , we use SonarQube to verify and test the application and everything goes good, then finally we will create a "Docker Image" and we will push this Docker Image" to the Docker Registry like to ECR or DockerHub. 


And at the end of the "Continuous Integration process, we have a Image ready with the tag and once the Image gets pushed, how does the CD gets triggered, CD ->   and the best continuous delivery tools in the market are "Gitops" based tools and what "gitops" based tools say, similar to your source code, you should also create a Git repository and this will have a "Application Manifest" and this application manifest is nothing but Kubernetes "pod.yml, deployment.yml,service,yml" . 


-> Now, you created a new Image version in your CI pipeline and the question is how will your "Argo Cd or Gitops tool" come to know there is a new image in the registry or any Helm chart should be updated, for this we have two ways, one is we have a very good tool called as "Argo Image Updater" will continuously monitor the "Dockerhub or container registries" and whenever a new Image is pushed to your container registry, it will notify and directly update the Git repository with the new version  in the pod.yml. Deployment.yml or if your using helm charts also it have capability to update the changes in Helmcharts as well. 

-> Argo Image Updater - step 1.  monitoring the container registries and step 2.  It is updating the Github repository .

And then we have the "ArgoCD" which is continuously watching the "Git Repository" and it says whenever there is a change in pod.yml. Deployment.yml , take these new files and deploy them to the Kubernetes cluster . 



-> In a nutshell, CD process is as soon as the new Docker image process is completed, and after the Image is pushed to the Docker Registry or Container Registry then we have the tool called "Argo Image Updater"  or we can also use "Shell Scripts" here and for now Argo Image Updater which watches for the new changes in the Application Manifest Git Repository and updates them continuously and then "ArgoCD" which is sitting inside the "Kubernetes Cluster" and which is Kubernetes Controller and which always try to maintain the state between the Git repository and a Kubernetes Cluster and whenever there is a new Image or whenever there is a new Volume or new Mount, anything  that you change for these resources , ArgoCD is capable of picking of those changes and deploying them in Kubernetes Cluster . 



