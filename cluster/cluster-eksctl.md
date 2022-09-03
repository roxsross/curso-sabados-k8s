eksctl create cluster -f cluster-demo.yaml

aws eks --region us-east-1 update-kubeconfig --name fargate-cluster

### OIDC
eksctl utils associate-iam-oidc-provider --region=us-east-1 \
  --cluster fargate-cluster  \
  --approve

curl -o alb_iam_policy.json https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/release-2.4/docs/install/iam_policy.json  

### iam
aws iam create-policy \
    --policy-name AWSLoadBalancerControllerIAMPolicy2022 \
    --policy-document file://alb_iam_policy.json

eksctl create iamserviceaccount \
  --cluster fargate-cluster \
  --namespace kube-system \
  --name aws-load-balancer-controller \
  --attach-policy-arn arn:aws:iam::402135063963:policy/AWSLoadBalancerControllerIAMPolicy2022 \
  --override-existing-serviceaccounts \
  --approve    

  kubectl get sa aws-load-balancer-controller -n kube-system

https://artifacthub.io/packages/helm/aws/aws-load-balancer-controller

## helm instalacion:


helm repo add eks https://aws.github.io/eks-charts

helm upgrade -i aws-load-balancer-controller \
    eks/aws-load-balancer-controller \
    -n kube-system \
    --set clusterName=fargate-cluster \
    --set serviceAccount.create=false \
    --set serviceAccount.name=aws-load-balancer-controller \
    --set image.tag="v2.4.1" \
    --set region=us-east-1 \
    --set vpcId=vpc-0347139dbe4f1dee0 \
    --version="1.4.1"