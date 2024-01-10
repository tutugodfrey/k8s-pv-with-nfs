# Kubernetes Persistent Volumes with NFS

How to use an nfs server for kubernetes storage

To be able to use nfs storage in your cluster the nodes on the cluster should have nfs-client (e.g nfs-common) install

```bash
apt install nfs-common
```

To use nfs-subdir-external-provisioner

```bash
helm repo add nfs-subdir-external-provisioner https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner/
helm install nfs-subdir-external-provisioner nfs-subdir-external-provisioner/nfs-subdir-external-provisioner --set nfs.server=54.165.249.27 --set nfs.path=/data --set namespace=kube-system
```


```bash
Annotations:   volume.beta.kubernetes.io/storage-provisioner: cluster.local/nfs-subdir-external-provisioner
               volume.kubernetes.io/storage-provisioner: cluster.local/nfs-subdir-external-provisioner
Finalizers:    [kubernetes.io/pvc-protection]
Capacity:      
Access Modes:  
VolumeMode:    Filesystem
Used By:       sentry-clickhouse-0
Events:
  Type     Reason                Age                   From                                                                                                                                 Message
  ----     ------                ----                  ----                                                                                                                                 -------
  Normal   ExternalProvisioning  4m38s (x42 over 14m)  persistentvolume-controller                                                                                                          Waiting for a volume to be created either by the external provisioner 'cluster.local/nfs-subdir-external-provisioner' or manually by the system administrator. If volume creation is delayed, please verify that the provisioner is running and correctly registered.
  Normal   Provisioning          44s (x4 over 2m30s)   cluster.local/nfs-subdir-external-provisioner_nfs-subdir-external-provisioner-85ccb6b887-2n5hs_e923ef37-5f6a-47b2-9a57-b382f8ba179f  External provisioner is provisioning volume for claim "default/sentry-clickhouse-data-sentry-clickhouse-0"
  Warning  ProvisioningFailed    44s (x4 over 2m30s)   cluster.local/nfs-subdir-external-provisioner_nfs-subdir-external-provisioner-85ccb6b887-2n5hs_e923ef37-5f6a-47b2-9a57-b382f8ba179f  failed to provision volume with StorageClass "nfs-client": unable to create directory to provision new pv: mkdir /persistentvolumes/default-sentry-clickhouse-data-sentry-clickhouse-0-pvc-94665d60-4920-44f4-93b6-e8dae33ff13a: permission denied

```