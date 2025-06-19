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

6. Click on ***demo*** application to see ***SYNC/LAST SYNC*** status:

![week4_task-last_6](../.data/week4_task-last_6.png "week4_task-last_6")

![week4_task-last_7](../.data/week4_task-last_7.png "week4_task-last_7")




  
    
