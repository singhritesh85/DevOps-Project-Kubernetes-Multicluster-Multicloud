# terraform-eks
```
1. First of all clone this repository and change the directory to "terraform-eks-withaddons".
2. Run the shell script initial-setup.sh only once on your k8s-management-node or terraform-server. As this script will install the kubectl, helm and uninstall awscli version 1.x then install awscli version 2.x. After running this shell script just logout from the logged-in user and then login again.
3. Finally you can create the different environment depending on your need using this terraform script.
```   

# Install and configure EKS Container Insight 
```
curl https://raw.githubusercontent.com/aws-samples/amazon-cloudwatch-container-insights/latest/k8s-deployment-manifest-templates/deployment-mode/daemonset/container-insights-monitoring/quickstart/cwagent-fluentd-quickstart.yaml | sed "s/{{cluster_name}}/cluster-name/;s/{{region_name}}/cluster-region/" | kubectl apply -f -
```

In this command, cluster-name is the name of your Amazon EKS or Kubernetes cluster, and cluster-region is the name of the Region where the logs are published. We recommend that you use the same Region where your cluster is deployed to reduce the AWS outbound data transfer costs.

```
curl https://raw.githubusercontent.com/aws-samples/amazon-cloudwatch-container-insights/latest/k8s-deployment-manifest-templates/deployment-mode/daemonset/container-insights-monitoring/quickstart/cwagent-fluentd-quickstart.yaml | sed "s/{{cluster_name}}/eks-demo-cluster-dev/;s/{{region_name}}/us-east-2/" | kubectl apply -f -
```

Then go to EC2 Instance created as a part of NodeGroup of this EKS Cluster and open it's IAM Role and attach the policy CloudWatchLogsFullAccess . Finally go to Cloudwatch Console, Open Insights > Container Insights. 



Reference:- https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Container-Insights-setup-EKS-quickstart.html

# terraform-aks

To create Application Gateway Ingress Controller make sure the Managed Identity **ingressapplicationgateway-aks-cluster** sholud have below accesses
```
(a) At least Reader access for the resource group in which Application Ingress Controller exists.
(b) Contributor access for the Application Ingress Controller.
```
<br> <br/>
![image](https://github.com/singhritesh85/terraform-azure/assets/56765895/7380c694-81bd-43dd-83be-61c45d952783)
<br> <br/> <br> <br/>
**In this terraform script it has been achieved using as written below**
<br> <br/>
![image](https://github.com/singhritesh85/terraform-azure/assets/56765895/1f158295-c45b-4663-b081-1922b199881b)

<br><br/>
Please provide the information in the terraform script as wriiten below
1. Use your own .pfx file in main directory and provide it's password in file module/application-gateway.tf.
2. Provide public SSH key in the files custom_data_devopsagent.sh, custom_data_blackboxexporter.sh, custom_data_grafana.sh, custom_data_loki.sh, custom_data_prometheus.sh and custom_data_sonarqube.sh.
3. Provide tenant id and subscription id in the file provider.tf.
