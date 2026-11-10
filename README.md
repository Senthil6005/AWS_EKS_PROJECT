## AWS Application Load Balancer setup steps:
=============================================
1. Tags all the subnet with the following tags:

   1.1 For Private subnet:
         - ```key - kubernetes.io/role/internal-elb``` 
         - ```value - 1 ```
           
   1.2 For Public subnet:
       - ```key - kubernetes.io/role/elb```
       - ```value - 1 ```
         

2. Create IAM Policy for AWS Load Balancer Controller. 
   
   2.1 Get policy document using command : 
       ``` 
       curl -O https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.5.4/docs/install/iam_policy.json
       ```
       
   2.2 Apply the policy using command :
      ``` 
             aws iam create-policy \
            --policy-name AWSLoadBalancerControllerIAMPolicy \
            --policy-document file://iam_policy.json 
        ```

3. Install eksctl , kubectl , Helm (if not already)

  3.1 Install EKSCTL using command : 
        ``` 
curl --silent --location \
"https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" \
| tar xz -C /tmp

mv /tmp/eksctl /usr/local/bin/eksctl

eksctl version

        ``` 
============

  3.2 Install KUBECTL using command : 

         ``` 
curl -LO "https://dl.k8s.io/release/v1.30.0/bin/linux/amd64/kubectl"

chmod +x kubectl

mv kubectl /usr/local/bin/kubectl

kubectl version --client

        ``` 
============

  3.3 Install HELM using command : 
  
    ``` 
curl -fsSL -o get_helm.sh \
https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-4

chmod 700 get_helm.sh 

# ./get_helm.sh

# helm version

    ``` 
============
