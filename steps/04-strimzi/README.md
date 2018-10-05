# Strimzi – Kafka Cluster

Also see: 

  * http://strimzi.io/

---

**Sed for OSX**

`sed` for OSX works differently than on Linux, the easiest way around it to use gnu-sed tool:

    brew install gnu-sed

You then need to replace `sed` later on with `gsed`.

---

## Deploy Strimzi

    sed -i 's/namespace: .*/namespace: strimzi/' strimzi/examples/install/cluster-operator/*ClusterRoleBinding*.yaml

    oc login -u admin

    oc new-project strimzi --display-name='Strimzi'
    oc create -f strimzi/examples/install/cluster-operator
    oc create -f strimzi-admin.yml
    oc set env deployment/strimzi-cluster-operator STRIMZI_NAMESPACE=strimzi,kafka

    oc adm policy add-cluster-role-to-user StrimziAdmin developer

    oc login -u developer

## Create Kafka cluster

    oc new-project kafka  --display-name='Kafka Cluster'
    oc apply -f kafka
