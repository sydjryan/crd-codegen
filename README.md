# crd-codegen

Generates Go API interfaces for a Kubernetes Custom Resource by parsing its OpenAPI schema in the YAML `CustomResourceDefinition`. Useful if an operator/application was not written in Go but you have a need to interact with its resoures.

This is a **work in progress**. The JSON schema generators do not generate code that is fully-compatible with k8s controller-gen, however getting more of the process automated is in the works.

## Example usage

Using the Strimzi operator as an example:

```
# grab dependencies
go get
export PATH=$PATH:$(go env GOPATH)

# install go-jsonschema (https://github.com/omissis/go-jsonschema)
brew tap omissis/go-jsonschema
brew install go-jsonschema

# download CRD's for strimzi operator
VERSION=0.41.1
wget https://github.com/strimzi/strimzi-kafka-operator/releases/download/${VERSION}/strimzi-crds-${VERSION}.yaml

# generate types using the CRD
./generate.sh strimzi-crds-${VERSION}.yaml

# generated apis are found in 'generated' directory:
ls generated/apis/kafka.strimzi.io/v1beta2/

# Kafka.go  KafkaConnect.go  KafkaMirrorMaker.go  KafkaNodePool.go  KafkaTopic.go  KafkaBridge.go  KafkaConnector.go   KafkaMirrorMaker2.go   KafkaRebalance.go   KafkaUser.go
```
