# GC-Delay-Study
Extracting the google cloud delay distribution among the nodes

## Purpose
Due to the variety of issues that occur when deploying nodes on the cloud, such as scalability and reliability issues, we have conducted a study on the delay in communication between nodes in order to develop a more realistic way to simulate a SkipGraph without having to go through the hassle of deploying SkipNodes on the cloud.

## Methodology

### Deployment
In order to collect realistic network statistics, the Google Cloud Compute Engine service was used. Instances were deployed in multiple locations distributed all over the globe. Once the instances we deployed, SkipNodes were started and initialized on the instances. The instructions to launching the nodes can be found in the documentation for mass deployment.

### Testing 
Using the RemoteAccessTool, any one of the nodes in the SkipGraph can be accessed in order to start the testing. Once the testing starts, the tool traverses the graph in order to create a list of all the nodes in the SkipGraph. Once the list is complete, the tool makes every node in the list ping every other node X times. In order to spread the pinging attempts over a longer period, the tool allows the user to split the X pinging attempts into N equally sized chunks.

### Logging
The RemoteAccessTool will output a .CSV file that contains all the logs collected from the pinging attempts. The output file looks something like this:

|Pinger| 21 | | | | |
|--|--|--|--|--|--|
| Pinged | Avg Ping | StdDev | Individual Results |  |
| 1 | 48.3565 | 3.942893322 | 45 | 44 | 45 | 44 | 52 | 51 |
| 2 | 227.36625 | 4.502733718 | 225 | 226 | 227 | 227 | 226 | 225 |
| 3 | 36.939 | 4.129016711 | 33 | 33 | 36 | 37 | 76 | 37 |
| 4 | 235.16375 | 4.20153971 | 246 | 236 | 233 | 233 | 230 | 229 |
| 5 | 98.542 | 4.169860429 | 98 | 99 | 99 | 99 | 101 | 101 |

All nodes are identified by their name ID. The pinger is the node that is pinging other nodes. The 'Avg Ping' and the 'StdDev' fields are the average and the standard deviation of all the individual pinging attempts between the Pinger node and the Pinged node, respectively. Following that is the result of every single pinging attempt.

## Results
After setting up a network of 32 nodes, ping log collection was carried out. The logs can be found in the logs folder, along with the configuration files in order to replicate the same SkipGraph structure. The data from the logs has been translated to histograms (which can be found in the results folder). Two different types of histograms were created:

 - Histogram of the average RTT delay between every pair of nodes.
 - Histogram of all the recorded RTT delays between a single pair of nodes.

After the histograms were created, different distributions were fitted to see which ones resemble the histogram the best. A normal distribution appeared to be the closest fit for both types of histograms. As for the histogram of the average RTT delay between every pair of nodes, the fitting normal distribution had the following parameters:
- μ = 161.135
- σ = 97.073

As for the other type of histogram, the parameters are exactly as in the logs.


  
