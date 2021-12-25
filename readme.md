
### Schema Evaluation and mergeSchema option in Spark with a sample pyspark code.

![](image/schema-merge.png)


#### Version 1
```
+-----+--------+
|empid|   ename|
+-----+--------+
|  101| Sravana|
|  102| Lakshmi|
|  103| Sreekar|
|  104|  Vikram|
|  105|Srikriti|
|  101| Sravana|
|  102| Lakshmi|
|  103| Sreekar|
|  104|  Vikram|
|  105|Srikriti|
|  101| Sravana|
|  102| Lakshmi|
|  103| Sreekar|
|  104|  Vikram|
|  105|Srikriti|
+-----+--------+
```
#### Version 2
```
+-----+--------+-----------+
|empid|   ename|designation|
+-----+--------+-----------+
|  101| Sravana|   TechLead|
|  102| Lakshmi|   TechArch|
|  103| Sreekar|       Lead|
|  104|  Vikram|    Manager|
|  105|Srikriti|  Developer|
|  101| Sravana|   TechLead|
|  102| Lakshmi|   TechArch|
|  103| Sreekar|       Lead|
|  104|  Vikram|    Manager|
|  105|Srikriti|  Developer|
|  101| Sravana|       null|
|  102| Lakshmi|       null|
|  103| Sreekar|       null|
|  104|  Vikram|       null|
|  105|Srikriti|       null|
+-----+--------+-----------+
```
#### Version 3
```
+-----+--------+-----------+----------+
|empid|   ename|designation|department|
+-----+--------+-----------+----------+
|  101| Sravana|   TechLead|        IT|
|  102| Lakshmi|   TechArch|    Social|
|  103| Sreekar|       Lead|   Science|
|  104|  Vikram|    Manager| Marketing|
|  105|Srikriti|  Developer|        IT|
|  101| Sravana|   TechLead|      null|
|  102| Lakshmi|   TechArch|      null|
|  103| Sreekar|       Lead|      null|
|  104|  Vikram|    Manager|      null|
|  105|Srikriti|  Developer|      null|
|  101| Sravana|       null|      null|
|  102| Lakshmi|       null|      null|
|  103| Sreekar|       null|      null|
|  104|  Vikram|       null|      null|
|  105|Srikriti|       null|      null|
+-----+--------+-----------+----------+
```



#
#
#
$SPARK_HOME/bin/spark-submit \
--name "Sample Spark Application" \
--master local[*] \
--packages org.apache.spark:spark-streaming-kafka-0-8:2.4.0-cdh6.3.2 \
--conf "spark.executorEnv.PYSPARK_DRIVER_PYTHON=./venv/bin/python" \
--conf "spark.executorEnv.PYSPARK_PYTHON=./venv/bin/python" \
--py-files "file:///apps/hostpath/spark/artifacts/application.zip" /apps/hostpath/spark/artifacts/hello.py