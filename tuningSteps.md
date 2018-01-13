### Change based on relevance:

#### 1. File handle limits.
assuming logged in as root and on the kafka broker machine
This is to augment file handle limits for kafka.

echo "* hard nofile 100000
* soft nofile 100000" | tee -- append /etc/security/limits.conf


#### 2. Swappiness.

vim /etc/sysctl.conf
add vm.swappiness = 0
and then reboot vm.

When you log back
cat /proc/sys/vm/swappiness gives the changed value of vm.swappiness.


#### 3. Adjust JVM heap size.
editing kafka-server-start.sh, zookeeper-server-start.sh and so on:

eg:
CONFLUENT-3.1.2 kafka-console-producer
8 concurrent instances on machine (88 cores)
11 brokers
topic has 12 partitions and 1 replication factor

export KAFKA_HEAP_OPTS="-Xmx30G -Xms26G"
