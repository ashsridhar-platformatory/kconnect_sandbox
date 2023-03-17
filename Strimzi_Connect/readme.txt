1: Create a new namespace <namespace> in Kuberbenetes
2: Install Strimzi cluster operator in that namespace
   	kubectl create -f 'https://strimzi.io/install/latest?namespace=<namespace>' -n <namespace>
3: Apply cc_secret.yaml file
   This creates Kubectl secrets that will be used to connect to CC broker
   NOTE: Before applying, replace the placeholders with actual values
4: Apply aws-creds.yaml
   This sets up the AWS credentials for KafkaConnect to read as environment variables
   NOTE:Before applying, replace the placeholders with actual values
5: Apply connect_full.yaml
   This sets up the KafkaConnect strimzi resource. 
   This deployment uses a custom created docker image which is just a cp-connect base image built with additional plugins for JDBC and S3 sink connectors.
   The current setup points to a docker image in docker hub under the name "ashsridhar/strconnect-jdbc-s3:1.0.0". For extensions, any other similar image could be used with appropriate additions.
   It is important that "use-connector-resources" is set to true.
   NOTE:Before applying, replace the placeholders with actual values
6: Apply jdbc_sink.yaml
   This sets up the JDBC sink connector as strimzi CRD
   NOTE:Before applying, replace the placeholders with all configuration values
7: Apply s3_sink.yaml
   This sets up the S3 sink connector as strimzi CRD
   NOTE:Before applying, replace the placeholders with all configuration values
   
