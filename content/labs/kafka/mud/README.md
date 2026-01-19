# run me

## comannds

**create stack**

```bush
kubectl annotate storageclass gp3 storageclass.kubernetes.io/is-default-class=true 

oc create namespace kafka-mud

kubectl create secret docker-registry cloudera-registry-secret   --namespace kafka-mud   --docker-server container.repository.cloudera.com   --docker-username XX   --docker-password XX

```

**create kafka**

```bush
oc apply --filename kafka-mud.yml,kafkanodepool.yml --namespace kafka-mud



k9s -n kafka-mud

s for shell

/opt/kafka/bin/kafka-topics.sh --bootstrap-server mud-kafka-kafka-bootstrap:9092 --create --topic my-topic
/opt/kafka/bin/kafka-topics.sh --bootstrap-server mud-kafka-kafka-bootstrap:9092 --describe

/opt/kafka/bin/kafka-console-producer.sh --bootstrap-server mud-kafka-kafka-bootstrap:9092 --topic my-topic
/opt/kafka/bin/kafka-console-consumer.sh --bootstrap-server mud-kafka-kafka-bootstrap:9092 --topic my-topic --from-beginning
```

<details>

./kafka-topics.sh --bootstrap-server gre-smm-dh-corebroker2.cldr-gre.yovj-8g7d.cloudera.site:9093,gre-smm-dh-corebroker1.cldr-gre.yovj-8g7d.cloudera.site:9093,gre-smm-dh-corebroker0.cldr-gre.yovj-8g7d.cloudera.site:9093 --describe

./kafka-topics.sh --bootstrap-server localhost:9093 --describe

cat >/tmp/kafka-ssl.properties <<EOF
security.protocol=SASL_SSL
sasl.mechanism=GSSAPI
sasl.kerberos.service.name=kafka
ssl.truststore.location=/var/lib/cloudera-scm-agent/agent-cert/cm-auto-global_truststore.jks
ssl.truststore.password=LrMQGf408LC10V05SGa0e5SPb0
ssl.endpoint.identification.algorithm=
EOF

cat /tmp/kafka-ssl.properties
<summary><b>Click to expand fast commands for test datahub cli</b></summary>