Spark
=======

As of spark 2 there is not official support for _ec2_.

_Flintrock_ seems to be a great alternative.

```
$ pip3 install flintrock
```

## creating key pair

```
aws ec2 create-key-pair --key-name coursera-spark \
  --query 'coursera' \
  --output text > coursera-spark.pem
```
Lets check that we created it.

```
aws ec2 describe-key-pairs
```

## launching a cluster

```
flintrock launch test-cluster \
    --num-slaves 1 \
    --spark-version 2.2.0 \
    --ec2-key-name coursera-spark \
    --ec2-identity-file ~/.ssh/coursera-spark.pem \
    --ec2-ami ami-d834aba1 \
    --ec2-user ec2-user
```

## stopping a cluster

```
flintrock destroy test-cluster
```
