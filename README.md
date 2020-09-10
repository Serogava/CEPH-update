# Update CEPH v.10 to v.12

### You need doing next steps:
1. ```ceph osd set sortbitwise```
2. ```ceph osd set noout```
3. ```sudo yum install ceph-deploy```
4. ```ceph-deploy install --release luminous $node1 $node2 $node3```
5. all nodes: ```systemctl restart ceph-mon.target```

### If you can't see mgr node, you need add it.

6. ```ceph auth get-or-create mgr.$node1 mon 'allow profile mgr' osd 'allow *' mds 'allow *'
   mkdir /var/lib/ceph/mgr/ceph-$node1
   vi /var/lib/ceph/mgr/ceph-$node1/keyring
   ceph-mgr -i $node1```
7. ```ceph auth get-or-create mgr.$node2 mon 'allow profile mgr' osd 'allow *' mds 'allow *'
   mkdir /var/lib/ceph/mgr/ceph-$node2
   vi /var/lib/ceph/mgr/ceph-$node1/keyring
   ceph-mgr -i $node2```
8. ```ceph auth get-or-create mgr.$node3 mon 'allow profile mgr' osd 'allow *' mds 'allow *'
   mkdir /var/lib/ceph/mgr/ceph-$node3
   vi /var/lib/ceph/mgr/ceph-$node3/keyring
   ceph-mgr -i $node3```

9. all nodes: ```systemctl restart ceph-osd.target```
10. ```ceph osd require-osd-release luminous```
11. ```ceph osd unset noout```