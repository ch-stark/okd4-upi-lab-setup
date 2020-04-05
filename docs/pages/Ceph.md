## Ceph setup

    mkdir -p ${OKD4_LAB_PATH}/ceph
    sed "s|%%LAB_DOMAIN%%|${LAB_DOMAIN}|g" ./Provisioning/Ceph/cluster.yml > ${OKD4_LAB_PATH}/ceph/cluster.yml
    cp ./Provisioning/Ceph/common.yml ${OKD4_LAB_PATH}/ceph/common.yml 
    cp ./Provisioning/Ceph/operator-openshift.yml ${OKD4_LAB_PATH}/ceph/operator-openshift.yml

    oc apply -f ${OKD4_LAB_PATH}/ceph/common.yml
    oc apply -f ${OKD4_LAB_PATH}/ceph/operator-openshift.yml
    oc apply -f ${OKD4_LAB_PATH}/ceph/cluster.yml