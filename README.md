# kconnect_sandbox
Turnkey Kafka Connect Sandbox
------------REQUIREMENTS-------------------------:

Set up a turnkey Kafka Connect sandbox: Work with 
@Avinash Upadhyaya
 to make this a single helm chart
Allows you to set up connectors, load /path/to/jar drop in and get's loaded into plugin.path - by default
Point it at brokers
Comes with a built-in prometheus + grafana dashboard against JMX exporter metrics
Based on this setup, run this on a standard 3-node connect cluster
Study JDBC connector in atleast 2 modes
Bulk / Table mode
Timestamp + Incrementing mode
....with a script to create load on the database (must generate both inserts and updates) at a configurable rate
Study in each case and analyze
JMX metrics
Throughput on the topic
Latency against each record sampled
Make recommendations (in general, particularly related to connectors) on optimizing for
Throughput
Latency

-------------REQUIREMENTS----------------------------

Deliverables
1: Helm chart
2: Report on studying JDBC Conenctor	
3: Load script


Activity log:
1. Have Kubernetes cluster up and running (3 nodes EKS from AWS)
2. create namespace monitoring and setup Prometheus and Grafana
	curl -s https://raw.githubusercontent.com/coreos/prometheus-operator/master/bundle.yaml | sed -e '/[[:space:]]*namespace: [a-zA-Z0-9-]*$/s/namespace:[[:space:]]*[a-zA-Z0-9-]*$/namespace: monitoring/' > prometheus-operator-deployment.yaml
	kubectl create namespace monitoring
	kubectl create -f prometheus-operator-deployment.yaml -n monitoring
All the strimzi setup
	Now the connector is running in the sandbox
kubectl create secret generic additional-scrape-configs --from-file=prometheus-additional.yaml -n monitoring (TAG)
sed -i 's/namespace: .*/namespace: my-namespace/' prometheus.yaml
kubectl apply -f strimzi-pod-monitor.yaml -n monitoring
kubectl apply -f prometheus-rules.yaml -n monitoring (TAG)
kubectl apply -f prometheus.yaml -n monitoring

Once all the pods are up and running, install grafana.yaml
kubectl apply -f grafana.yaml -n monitoring
Do port forwarding to a local port
Login to grafana dashboard with admin/password
add datasource as prometheus and enter the prometheus url which is http://prometheus-operated.monitoring:9090
Imported kafka connect dashboard provided by strimzi
--------------------------------------------------------------------------------
