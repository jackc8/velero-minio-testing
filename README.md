1. run `kubectl apply -f minio-k8s.yaml`
1. create `credentials-velero`
```
[default]
aws_access_key_id = admin
aws_secret_access_key = <Password>
```
1. run
```
velero install \
    --provider aws \
    --plugins velero/velero-plugin-for-aws:v1.2.1 \
    --bucket velero \
    --secret-file ./credentials-velero \
    --use-volume-snapshots=false \
    --backup-location-config region=minio,s3ForcePathStyle="true",s3Url=http://s3.192.168.0.9.nip.io
```
1. run `kubectl get backupstoragelocations.velero.io -n velero default`
