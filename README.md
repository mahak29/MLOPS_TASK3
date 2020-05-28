# ML-Ops *(Integrating Machine Learning with Devops)*

“ **MLOps** (a compound of Machine Learning and “information technology operation”) is new discipline/focus/practice for collaboration and communication between data scientists and information technology (IT) professionals while automating and productizing machine learning algorithms.” 

![mlops structure](https://www.c-sharpcorner.com/UploadFile/BlogImages/11122019223851PM/image1.png)

Here I would like to share `my hands-on experience` while integrating *MLOps*

In these task I used 
- Docker 
- GitHub
- Jenkins

(Docker and Jenkins inside Virtual OS RHEL8)

##### So let's get into the jobs

1. Create container image that’s has Python3 and Keras or numpy  installed  using dockerfile 

2. When we launch this image, it should automatically starts train the model in the container.

3. Create a job chain of job1, job2, job3, job4 and job5 using build pipeline plugin in Jenkins 

4.  Job1 : Pull  the Github repo automatically when some developers push repo to Github.

5.  Job2 : By looking at the code or program file, Jenkins should automatically start the respective machine learning software installed interpreter install image container to deploy code  and start training( eg. If code uses CNN, then Jenkins should start the container that has already installed all the softwares required for the cnn processing).

6. Job3 : Train your model and predict accuracy or metrics.

7. Job4 : if metrics accuracy is less than 80%  , then tweak the machine learning model architecture.

8. Job5: Retrain the model or notify that the best model is being created

9. Create One extra job job6 for monitor : If container where app is running. fails due to any reason then this job should automatically start the container again from where the last trained model left

## Working on the task

* Creating 2 Dockerfile containing all the requirements modules for  **Traditional Machine Learning** and **Deep Learning**

<u>For both type of models create this Dockerfile</u>

1. Dockerfile with requirements
        
     <br><img src="/SS/ml1.png" width="1555" height="400">
      
2. Dockerfile which will run the code
        
     <br><img src="/SS/ml2.png" width="1555" height="400">
     
* Now have a look on the `desired`  *JOBS* (Screenshots are provided)

**I also use the COPY ARTIFACTS plug-ins as I'm facing problem while fetching the files from one job to another(It's your choice if ypu are not facing then don't use)**

1. **JOB 1** : Pull  the Github repo automatically when some developers push repo to Github.
  
      Give your GitHub Repository link  
      <br><img src="/SS/job1.1.png" width="1555" height="400">
      
      ADD the files to the base OS folder and have the trigger which we pull from the github
      
      <br><img src="/SS/job1.2.png" width="1555" height="400">
      
      <br><img src="/SS/job1.3.png" width="1555" height="400">

2. **JOB 2** : By looking at the code or program file, Jenkins should automatically start the respective machine learning software installed interpreter install image container to deploy code  and start training( eg. If code uses CNN, then Jenkins should start the container that has already installed all the softwares required for the cnn processing).

     It will run after job1 successfully build and copy the files from the job1

     <br><img src="/SS/job2.1.png" width="1555" height="400">
     
     Here I provided a python file and this will start the desired container according to the file (whether it is of CNN ot traditional machine learning)

     <br><img src="/SS/job2.2.png" width="1555" height="400">
     
     Grab the desired container
     
     <br><img src="/SS/container.png" width="1555" height="400">

3. **JOB 3** :  Train your model and predict accuracy or metrics.

     It will run after job2 successfully build and copy the files from the job1

     <br><img src="/SS/job3.1.png" width="1555" height="400">
      
     Now it start running the model and get the accuracy
     
     <br><img src="/SS/job3.2.png" width="1555" height="400">
     
     
     
 
         
        
