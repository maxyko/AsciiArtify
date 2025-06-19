# MVP: ArgoCD App creation

## How to create ArgoCD App with automatic synchronization

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


## Test run of ArgoCD Demo Application:

![week4_task-last_2](../.data/week4_task-last_2.gif)

Use ***port-forward*** to forward local port ***8088*** to ArgoCD Application port ***80*** :
```
kubectl port-forward -n demo svc/ambassador 8088:80 &
```

Download some test image:
```
wget -O ./g.png  https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png
```

Send test image using ***curl** utility to an application endpoint:
```
$ curl -F 'image=@g.png' localhost:8088/img/

Handling connection for 8088
  .;1tttt1i.                               ;:
 if1:....:i.                              .1;
iL;             ,;;;:    .;ii;,    :ii;:;, 1;  ,;;:,
ff.   .1tt11:. 11:::11, if1::if1 .tf;:;tL1 1; i1::;t1.
;Li       .tL.it     t1,Li    ;L,,L.    fi 1:.t;:;;:,.
 ;fti:,,,;tf: :ti,.,;t:.tf;,,:ff..ft:,,iLi 1; 1t;,.::
   :i1111i:    .;iii;,   :1111;.  .;11i;L1 ;, .:;iii:
                                 .11,,,1L:
```










  
    
