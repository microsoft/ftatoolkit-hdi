
## <img src="Assets/images/hdinsightpl.png" alt="FTA Toolkit: HDInsight Deployment Accelerator" style="float: left; margin-right:10px;" />
&nbsp;

### HDInsight Cluster Using Private Link Deployment Accelerator
 If you're ever in need of deploying an HD Insight Kafka Cluster using Private Endpoints here is an AZ CLI script that will walk you through the process. Getting HD Insight to work with Private Endpoints can be a bit tricky, so to make it easier here is an Azure CLI Script that will walk you through the process of creating your Resource Group, VNet, Subnets, Storage Account, NAT Gateway, HDInsight Kafka Cluster, Edge Node, Private Endpoints, DNS Configuration and VM to login and test the cluster access.

[For additional documentation click here](https://learn.microsoft.com/en-us/azure/hdinsight/hdinsight-private-link)

### Preparation
1. Install Azure CLI  
https://docs.microsoft.com/en-us/cli/azure/install-azure-cli
1. Clone repository / copy files locally
1. Edit the Variables Section inside the 'HDI_Kafka_Deploy.azcli' file 

    ```
        #----------------------------Variables-----------------------------------#
        #region Login
        $Location="eastus"
        $RG="AZU-HDI-PE-RG"
        $Sub="YOURSUBSCRIPTIONID" 
    
        # Network
        $NSG="hdi-kafka-vnet-nsg"
        $vNet="KafkaVNet"
        $sNet_HDI="HDISubnet"
        $sNet_Blob="StorageSubnet"
        $vNet_Client="hdi-privlink-client-vnet" 
        $sNet_Client="default"
    
        # Storage
        $STA="YOURSTORAGEACCOUNT"
        $Container="kafka"
    
        #NAT Gateway
        $Gateway="hdi-kafka-pl-nat-gateway"
        $Gateway_PublicIP="pip-ngw-hdi-kafka"
    
        # HDInsight Clusters
        $clusterName="hdi-bts-kafka-cluster" #Your Cluster Name must be unique
        $clusterType="kafka" #You can change this Hadoop if you want to deploy Hadoop
        #componentVersion="kafka=2.4" "You can change this Hadoop=3.1.0 if you want to deploy a Hadoop Cluster
        $httpCredential="YOURSECUREPASSWORDHERE"
        $clusterSizeInNodes="3"
        #clusterSizeMin="3"
        #clusterSizeMax="5"
        $sshCredentials="YOURSECUREPASSWORDHERE"
        $clusterVersion="5.0"
    
        #ssh sshuser@hdi-bts-kafka-cluster-ssh.azurehdinsight.net
        #https://hdi-bts-kafka.azurehdinsight.net
        #endregion
    ```

1. Edit the parameter file 'azuredeploy.parameters.json'
    ```
    {
        "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "clusterName": {
              "value": "YOURHDICLUSTERNAME" //YOUR HDI CLUSTER NAME
            },
            "EdgeNodeVirtualMachineSize": {
              "value": "Standard_E4_v3" //Change this to another VM size if you woud like
            }
        }
    }
    ```
1. Open the HDI_Kafka_Deploy.azcli file
1. Login to Azure using a Service Principal or interactively
1. Run each AZCLI command line by line
1. At the end of it you will have an HDInsight Cluster Running with Private Endpoints

#### Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.