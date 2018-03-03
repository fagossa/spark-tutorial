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

A key called `coursera-spark` must be present. If it is not the case you must create it the AWS console.

### Checking the AMI (optional)

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

## Stopping the machines
```
flintrock stop test-cluster
```

## Destroying the machines (when needed)
```
flintrock destroy test-cluster
```

----

## 5. Up and running

We can now get into the master through a browser

```
http://<MASTER PUBLIC IP>:8080/
```

or _ssh_

```
ssh -i ~/.ssh/coursera-spark.pem ec2-user@<MASTER PUBLIC IP>
```
