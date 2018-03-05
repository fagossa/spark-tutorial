$ pyspark

# Temperature reading

## Creating 100 temperature in memory samples in farenheight

```python
import random
data = [-9999] * 10 + [random.randint(-10, 110) for i in xrange(90)]
random.shuffle(data)
print(data)
```

## Distributing data across the cluster using RDDs

```python
d = sc.parallelize(data)
print(d)
```

## Actions on RDDs

```python
# creating a RDD
d.take(5)
d.takeSample(False, 5) #without replacement
d.first()
d.takeOrdered(5) # top 5 ordered elements
d.mean()

# Filtering and mapping data
dnomissing = d.filter(lambda x: x > -9999)
dnomissing.count()
dnomissingC = d.filter(lambda x: x > -9999).map(lambda x: (x-32)*5.0/9.0)
dnomissingC.mean()

# All in one using flatmap
d.flatMap(lambda x: [(x-32)*5.0/9.0] if x > -9999 else []).mean()
```
