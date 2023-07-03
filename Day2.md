## Deployment Strategies
We have mainly 2 deployment Strategies i.e., Recreate and Rolling Updates.
Rolling Update is the default one which K8 follows if you do not mwntion any specific type.

## Recreate:
In this Strategy, When any update is made to an deployment like changing an image or anversion/tag within an image. 
It will first terminate all the pods within the cluster and then create new pods, so there will be some downtime.

## Rollback:
In this Strategy, new pod will come one by one and old pods will be deprecated one by one, so that there will be no downtime for users accessing that application.

Example: When you want to change a image in deployment, you can do this by 2 options:
i) Edit yaml file and then apply kubectl apply.
ii)Declrative type: ''' kubectl set image deployment/deployment-name <image_name> '''
