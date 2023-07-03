## Deployment Strategies
We have mainly 2 deployment Strategies i.e., Recreate and Rolling Updates.
Rolling Update is the default one which K8 follows if you do not mwntion any specific type.

## Recreate:
In this Strategy, When any update is made to an deployment like changing an image or anversion/tag within an image. 
It will first terminate all the pods within the cluster and then create new pods, so there will be some downtime.

## Rolling:
In this Strategy, new pod will come one by one and old pods will be deprecated one by one, so that there will be no downtime for users accessing that application.

Example: When you want to change a image in deployment, you can do this by 2 options:
i) Edit yaml file and then apply kubectl apply.
ii)Declrative type:    kubectl set image deployment/deployment-name <image_name> 

## Rollback:
We can use this command to rollback to previous versions.
command: kubectl rollout undo deployment/<deployment-name>

We can also use rollout status and rollout history commands to get status and history of deployments.

### Commands & Arguments
 In a Dockerfile, CMD is the default parameter passed to the command whereas
 ENTRYPOINT is the command that is passed at the start of the command.

 In case of CMD Instruction, the Command line parameters passed will get replaced entirely.
 '''
 FROM Ubuntu
 CMD ["sleep", "5"]
 '''
 Docker command while runnig container: docker run ubuntu sleep 10
 The command that is passed at startuyp : sleep 10

 In case of Entrypoint, the command line parameters will get appended.
 '''
 FROM Ubuntu
ENTRYPOINT ["sleep"]
entrypoint ["5"]
'''
 Docker command while runnig container: docker run ubuntu sleep 10
 The command that is passed at startuyp : sleep 5

 If you want
