# Two Clusters in One VPC

The motivation for having two clusters in a single VPC is that your
persistent data is often in PostgreSQL or other data store that's
located in the VPC. If one cluster is hosed you can spin up another
without having to migrate your data to another vpc.

For this to work you need to create the VPC prior to calling eksctl
because you need 4 public and 4 private subnets in your vpc.

In aws console choose "create vpc" and select "vpc and more".

You need to enable auto assign public ip on your public subnets after
creating the vpc. There is no option for that during creation.

In your config make sure you have at least 2 public subnets (from
different availability zones). Same for private subnets.

Then just run the following.

```sh
eksctl create cluster -f cluster-one.yaml
eksctl create cluster -f cluster-two.yaml
```

You now have two k8s clusters in a single vpc. Assume you could have
as many as you want with enough subnets.