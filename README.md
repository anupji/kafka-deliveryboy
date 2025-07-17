# kafka-deliveryboy
https://youtu.be/ei6fK9StzMM

STEP-1
FOR /F "delims=" %i IN ('.\bin\windows\kafka-storage.bat random-uuid') DO SET KAFKA_CLUSTER_ID=%i
SET KAFKA_CLUSTER_ID=ZiqgSQTAS4exR-Qitaibug

STEP-2
.\bin\windows\kafka-storage.bat format --standalone -t %KAFKA_CLUSTER_ID% -c .\config\kraft\server.properties

C:\kafka>.\bin\windows\kafka-storage.bat format --standalone -t %KAFKA_CLUSTER_ID% -c .\config\kraft\server.properties
Formatting dynamic metadata voter directory /tmp/kraft-combined-logs with metadata.version 3.9-IV0.

STEP-3
.\bin\windows\kafka-server-start.bat .\config\kraft\server.properties

STEP-4
bin\windows\kafka-topics.bat --bootstrap-server localhost:9092 --create --topic NewTopic --partitions 3 --replication-factor 1

STEP-5
bin\windows\kafka-console-producer.bat --topic NewTopic --bootstrap-server localhost:9092

STEP-6
bin\windows\kafka-console-consumer.bat --topic NewTopic --from-beginning --bootstrap-server localhost:9092

bin\windows\kafka-dump-log.bat --cluster-metadata-decoder --files c:\tmp\kraft-combined-logs\__cluster_metadata-0\00000000000000000000.log

bin\windows\kafka-metadata-quorum.bat --bootstrap-server localhost:9092 describe --status
bin\windows\kafka-metadata-quorum.bat --bootstrap-server localhost:9092 describe --replication