## JsonPath
With JSON Path queries, you can customize, filter and format the output of a command as you like.

Using JSON Path commands in Kubectl:
1. kubectl get pods -o json
2. kubectl get nodes -o json
3. kubectl get pods -o=jsonPath='{ .items[0].spec.containers[0].image}'   // Command to get the Docker image for that Pod.
4. kubectl get pods -o=jsonPath='{ .items[0].metadata.name}'   // Command to get the Nodes
5. kubectl get pods -o=jsonPath='{ .items[0].status.nodeInfo.architecture}'   // Command to get the Hardware Architecture of Nodes.
6. kubectl get pods -o=jsonPath='{ .items[0].status.capacity.CPU}'   // Command to get the count of CPU on these Nodes.

You can also add multiple queries together:
- kubectl get nodes -o=jsonPath='{query1}{"\n}{query2}'

## Custom Columns
1. kubectl get nodes -o=custom-columns=<COLUMN NAME>:<JSON PATH>
2. kubectl get nodes -o=custom-columns=NODE: .metadata.name, CPU: .status.capacity.CPU

## Sort
1. kubectl get nodes --sort-by=.metadata.name          //sorts by name
2. kubectl get nodes --sort-by=.status.capacity.CPU    // sorts by CPU size
