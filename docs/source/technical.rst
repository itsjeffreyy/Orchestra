Technical Documentation
=======================


We use these projects:

.. figure:: projects_used.png
   :alt: projects

   projects

Running workshop monitoring
---------------------------

.. figure:: grafana.png
   :alt: grafana

   grafana

A snapshot of a running infrastructure:

.. figure:: gke_running_snapshot.png
   :alt: infrastructure

   infrastructure

Prometheus monitoring
---------------------

.. code:: shell

    helm install prometheus stable/prometheus

.. code:: shell

    NAME: prometheus
    LAST DEPLOYED: Tue Jul 28 20:02:17 2020
    NAMESPACE: default
    STATUS: deployed
    REVISION: 1
    TEST SUITE: None
    NOTES:
    The Prometheus server can be accessed via port 80 on the following DNS name from within your cluster:
    prometheus-server.default.svc.cluster.local


    Get the Prometheus server URL by running these commands in the same shell:
      export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=server" -o jsonpath="{.items[0].metadata.name}")
      kubectl --namespace default port-forward $POD_NAME 9090


    The Prometheus alertmanager can be accessed via port 80 on the following DNS name from within your cluster:
    prometheus-alertmanager.default.svc.cluster.local


    Get the Alertmanager URL by running these commands in the same shell:
      export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=alertmanager" -o jsonpath="{.items[0].metadata.name}")
      kubectl --namespace default port-forward $POD_NAME 9093
    #################################################################################
    ######   WARNING: Pod Security Policy has been moved to a global property.  #####
    ######            use .Values.podSecurityPolicy.enabled with pod-based      #####
    ######            annotations                                               #####
    ######            (e.g. .Values.nodeExporter.podSecurityPolicy.annotations) #####
    #################################################################################


    The Prometheus PushGateway can be accessed via port 9091 on the following DNS name from within your cluster:
    prometheus-pushgateway.default.svc.cluster.local


    Get the PushGateway URL by running these commands in the same shell:
      export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=pushgateway" -o jsonpath="{.items[0].metadata.name}")
      kubectl --namespace default port-forward $POD_NAME 9091

    For more information on running Prometheus, visit:
    https://prometheus.io/

Grafana
~~~~~~~

.. code:: shell

    helm search repo graphana
    helm inspect values stable/grafana > grafana/values.yaml

.. code:: shell

    kubectl create secret generic orchestra-password \
        --from-literal='orchestra-password=<MYPASSWORD>'

Google Kubernetes Cluster
-------------------------

Resizing a cluster
~~~~~~~~~~~~~~~~~~

To `resize a cluster’s node
pools <https://cloud.google.com/kubernetes-engine/docs/how-to/resizing-a-cluster>`__,
run the following command:

.. code:: shell

    gcloud container clusters resize cluster-name --node-pool pool-name \
        --num-nodes num-nodes

Replace the following:

-  cluster-name: the name of the cluster to resize.
-  pool-name: the name of the node pool to resize.
-  num-nodes: the number of nodes in the pool in a zonal cluster. If you
   use multi-zonal or regional clusters, num-nodes is the number of
   nodes for each zone the node pools is in. Repeat this command for
   each node pool. If your cluster has only one node pool, omit the
   –node-pool flag.

For more information, refer to the `gcloud container
clusters <https://cloud.google.com/sdk/gcloud/reference/container/clusters/resize>`__
resize documentation.
