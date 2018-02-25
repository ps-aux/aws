# Container for using Kubernetes on AWS with Kops

## Prerequisites

- Bash
- Docker with Docker Compose
- AWS account
- awscli installed and setup
- default SSH setup

Run `/kops.sh`

More info: https://github.com/kubernetes/kops/blob/master/docs/aws.md

##Quick setup:

#### Prepare name and S3 state storage
```
#Name the cluster (must end with `k8s.local`)
export NAME=my-cluster.k8s.local
aws s3api create-bucket \
    --bucket ${NAME} \
    --region eu-central-1 \
    --create-bucket-configuration LocationConstraint=eu-central-1
export KOPS_STATE_STORE="s3://${NAME}"
```
#### Create and customize cluster
```
kops create cluster --zones eu-central-1a ${NAME}
kops edit cluster ${NAME}
```
#### Customize instances config
```
kops edit ig nodes --name=${NAME}
kops edit ig master-eu-central-1a --name=${NAME}
```

If playing around you migh want to set the instances to `t2.micro` to be eligeble for free tier.

#### Build cluser
```
kops update cluster ${NAME} --yes
```

Now you can use `kubectl' to do stuff.


### SSH to EC2 isntances
Your default key @ `~/.ssh/id_rsa` is used as a key pair for the instances
```
ssh admin@<ip-address>
```

