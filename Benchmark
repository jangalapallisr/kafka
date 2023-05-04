VERSION:
./kafka-topics.sh --bootstrap-server kafka1:9092,kafka2:9092,kafka3:9092 --version
CREATE TOPIC:
 ./kafka-topics.sh --bootstrap-server="10.0.48.137:9092 10.0.67.162:9092 10.0.149.52:9092" --command-config kafka.properties --create --topic dpt_test_1p1r --replication-factor 1 --partitions 1
./kafka-topics.sh --bootstrap-server="kafka1:9092 kafka2:9092 kafka3:9092"  --create --topic dpt-test-10p3r --replication-factor 3 --partitions 10

LIST OF TOPICS:
./kafka-topics.sh --bootstrap-server="10.0.48.137:9092 10.0.67.162:9092 10.0.149.52:9092" --command-config ic_aws_kafka.properties —list
./kafka-topics.sh --bootstrap-server="kafka1:9092 kafka2:9092 kafka3:9092"  —list

DESCRIBE ABOUT TOPIC:
./kafka-topics.sh --bootstrap-server="10.0.48.137:9092 10.0.67.162:9092 10.0.149.52:9092" --command-config ic_aws_kafka.properties --describe --topic dpt-test-10p3r
./kafka-topics.sh --bootstrap-server="kafka1:9092 kafka2:9092 kafka3:9092" --describe --topic dpt-test-10p3r

PRODUCER HIT:
./kafka-producer-perf-test.sh  --topic sj-test --num-records 100 --record-size 100 --throughput -1 --producer-props bootstrap.servers="10.0.48.137:9092 10.0.67.162:9092 10.0.149.52:9092" --producer.config kafka.properties --print-metrics
./kafka-producer-perf-test.sh  --topic sj-test --num-records 100 --record-size 100 --throughput -1 --producer-props bootstrap.servers="kafka1:9092 kafka2:9092 kafka3:9092" --print-metrics

CONSUMER HIT:
./kafka-consumer-perf-test.sh --topic sj-test --bootstrap-server="10.0.48.137:9092 10.0.67.162:9092 10.0.149.52:9092" --messages 1000 --consumer.config ic_aws_kafka.properties --print-metrics
./kafka-consumer-perf-test.sh --topic sj-test --bootstrap-server="kafka1:9092 kafka2:9092 kafka3:9092" --messages 1000 --print-metrics

/home/subbuj/kafka-bench-producer.sh aws 0 131072 all
/home/subbuj/kafka-bench-producer.sh ic 0 131072 all
if [ $1 == "aws" ]; then
	echo " AWS Cluster..."
./kafka-producer-perf-test.sh --topic dpt-test-100p3r-1mr-100kb --num-records 10000 --record-size 100000 --throughput -1  --producer-props bootstrap.servers="kafka1:9092 kafka2:9092 kafka3:9092" linger.ms=$2 batch.size=$3 acks=$4 --print-metrics |grep "10000 records sent\|producer-metrics:batch-size-avg\|producer-metrics:bufferpool-wait-ratio\|producer-metrics:record-queue-time-avg\|producer-metrics:outgoing-byte-rate\|producer-metrics:request-latency-avg"
#./kafka-producer-perf-test.sh --topic dpt-test-100p3r-1mr-100kb --num-records 10000 --record-size 100000 --throughput 10000 --producer-props bootstrap.servers="kafka1:9092 kafka2:9092 kafka3:9092" linger.ms=0 batch.size=16384 acks=all --print-metrics |grep "10000 records sent\|producer-metrics:batch-size-avg\|producer-metrics:bufferpool-wait-ratio\|producer-metrics:record-queue-time-avg\|producer-metrics:outgoing-byte-rate\|producer-metrics:request-latency-avg"
else
	echo " IC AWS Cluster..."
./kafka-producer-perf-test.sh --topic dpt-test-100p3r-1mr-100kb --num-records 10000 --record-size 100000 --throughput -1 --producer-props bootstrap.servers="10.0.48.137:9092 10.0.67.162:9092 10.0.149.52:9092" linger.ms=$2 batch.size=$3 acks=$4 --producer.config ic_aws_kafka.properties  --print-metrics |grep "10000 records sent\|producer-metrics:batch-size-avg\|producer-metrics:bufferpool-wait-ratio\|producer-metrics:record-queue-time-avg\|producer-metrics:outgoing-byte-rate\|producer-metrics:request-latency-avg"
#./kafka-producer-perf-test.sh --topic dpt-test-100p3r-1mr-100kb --num-records 10000 --record-size 100000 --throughput 10000 --producer-props bootstrap.servers="10.0.48.137:9092 10.0.67.162:9092 10.0.149.52:9092" linger.ms=0 batch.size=16384 acks=all --producer.config ic_aws_kafka.properties  --print-metrics |grep "10000 records sent\|producer-metrics:batch-size-avg\|producer-metrics:bufferpool-wait-ratio\|producer-metrics:record-queue-time-avg\|producer-metrics:outgoing-byte-rate\|producer-metrics:request-latency-avg"
fi	
