## Ceph setup

    mkdir -p ${OKD4_LAB_PATH}/ceph
    sed "s|%%LAB_DOMAIN%%|${LAB_DOMAIN}|g" ./Provisioning/Ceph/cluster.yml > ${OKD4_LAB_PATH}/ceph/cluster.yml
    cp ./Provisioning/Ceph/common.yml ${OKD4_LAB_PATH}/ceph/common.yml 
    cp ./Provisioning/Ceph/operator-openshift.yml ${OKD4_LAB_PATH}/ceph/operator-openshift.yml

    for i in 0 1 2
    do
      oc label nodes okd4-worker-${i}.${LAB_DOMAIN} role=storage-node
    done

    oc apply -f ${OKD4_LAB_PATH}/ceph/common.yml
    oc apply -f ${OKD4_LAB_PATH}/ceph/operator-openshift.yml
    oc apply -f ${OKD4_LAB_PATH}/ceph/cluster.yml
    oc apply -f ${OKD4_LAB_PATH}/ceph/ceph-storage-class.yml



oc create -f toolbox.yaml
oc -n rook-ceph get pod -l "app=rook-ceph-tools"
oc -n rook-ceph exec -it $(kubectl -n rook-ceph get pod -l "app=rook-ceph-tools" -o jsonpath='{.items[0].metadata.name}') bash




oc -n rook-ceph delete deployment rook-ceph-tools