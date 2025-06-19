# MVP: ArgoCD App creation

### How to create ArgoCD App with automatic synchronization

![week4_task-last](../.data/week4_task-last.gif)

1. Log into ArgoCD WebUI and click on ***New App*** (or ***Create Application***):

![week4_task-last_1](../.data/week4_task-last_1.png "week4_task-last_1")

2. Set these fields in ***GENERAL*** block:

    ***Application Name*** --> demo
   
    ***Project Name***     --> default
   
    ***SYNC POLICY***      --> Automatic

    ***PRUNE RESOURCES*** checkbox --> ✅

    ***SELF HEAL***       checkbox --> ✅

    ***AUTO-CREATE NAMESPACE      -->  ✅


![week4_task-last_2](../.data/week4_task-last_2.png "week4_task-last_2")

3. Set these fields in ***SOURCE*** block:

    ***Repository URL*** --> https://github.com/den-vasyliev/go-demo-app
   
    ***Revision***       --> HEAD

    ***Path***           --> helm

![week4_task-last_3](../.data/week4_task-last_3.png "week4_task-last_3")

4. Set these fields in ***DESTINATION*** block:

    ***Cluster URL***  --> https://kubernetes.default.svc
   
    ***Project Name*** --> demo

![week4_task-last_4](../.data/week4_task-last_4.png "week4_task-last_4")

5. Click on ***CREATE*** button --> ***demo*** application will be created and ***sync*** process will be started automatically:

![week4_task-last_5](../.data/week4_task-last_5.png "week4_task-last_5")

6. Click on ***demo*** application to see/check ***LAST SYNC/SYNC/APP HEALTH*** statuses - wait till they get ***green*** status:

![week4_task-last_6](../.data/week4_task-last_6.png "week4_task-last_6")

![week4_task-last_7](../.data/week4_task-last_7.png "week4_task-last_7")

![week4_task-last_8](../.data/week4_task-last_8.png "week4_task-last_8")

7. To test ArgoCD App with automatic synchronization, click for examply on ***ambassador*** service:

![week4_task-last_9](../.data/week4_task-last_9.png "week4_task-last_9")

![week4_task-last_10](../.data/week4_task-last_10.png "week4_task-last_10")

and scroll down till the ***LIVE MANIFEST***:

![week4_task-last_11](../.data/week4_task-last_11.png "week4_task-last_11")

8. Click on ***EDIT*** and change for example service type from ***NodePort*** --> ***LoadBalancer*** ; click on ***SAVE*** button and close the window:

![week4_task-last_12](../.data/week4_task-last_12.png "week4_task-last_12")

![week4_task-last_13](../.data/week4_task-last_13.png "week4_task-last_13")

9. Now you can see that after such changes automatic synchronization process was started and ArgoCD tries to get a state equal to the state described in a source repo:

![week4_task-last_14](../.data/week4_task-last_14.png "week4_task-last_14")

![week4_task-last_15](../.data/week4_task-last_15.png "week4_task-last_15")










  
    
