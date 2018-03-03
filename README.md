Spark in EC2
=======

As of spark 2 there is not official support for _ec2_.

## 1. Installing Flintrock

```
$ pip3 install flintrock
```

----

## 2. Checking your key-pair

```
aws ec2 describe-key-pairs
```

### Checking the AMI

```
aws ec2 describe-images --image-ids ami-0c824875 | jq
```

----

## 3. launching a cluster

```
flintrock launch test-cluster \
    --num-slaves 1 \
    --spark-version 2.2.0 \
    --ec2-key-name coursera-spark \
    --ec2-identity-file ~/.ssh/coursera-spark.pem \
    --ec2-ami ami-e5c84c96 \
    --ec2-user root
```

----

## 4. stopping a cluster

```
flintrock destroy test-cluster
```
