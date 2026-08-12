# CEPH



## Introduction 

Ceph, ceph is a distributed storage manager, ceph manages your logical disks, back up and replication of your data.  
In a simple way, ceph does some interesting things with your data. Ceph is offers three ways of storing data; these include:
	
- CephFS
	This is the ceph distributed file system built on top of ceph's distributed object store. The cephFS is POSIX compliant.

- Ceph Object storage
	Ceph object storage allows you to store data objects in a distributed manner.  
	This storage is also compatibe with S3 api, allowing apps to easily store and retrieve data in a cloud like environment
	

- Ceph Block device
	Well, a block device is a storage device that only writes block of memory into physical storage. The blocks can be of variable size  
	example, 512 bytes, 1kib, 2kib, 4kib. Ceph help you manage these.

Ceph uses the CRUSH (Controlled Replication Under scalable hashing) algorithm to calculate where data is located or where data is to be placed, the crush algorithm splits the storage area to placement groups.  Ceph calculates the placement group of a data object then places/finds the data to the appropriate PG. It further calculates which OSD daemon should store the placement group.  This algorithm allows the ceph Storage cluster to scale, rebalance and recover dynamically.

Another amazing thing about ceph is that, once a disk or an OSD daemon fails, it validates that the daemon has failed and reconstructs this lost data from the replicated and distributed data in the storage pool.

## Cephs Cluster

Since ceph is a storage cluster, it has several components that enable it to reliable store, back-up and ensure high availability of the cluster and the data.

### Components of the ceph cluster
It is made up of 
- Ceph OSDs (Object storage daemons)
	These exist for every logical disk, these daemons are responsible for data storage, data replication, recovery, rebalancing and providing some monitoring information to the ceph monitors and managers by checking for other ceph OSD daemons for a heartbeat.  
	Three OSD daemons are normally required for redundancy and high availability.

- __Ceph Monitors__
	Ceph monitors maintain maps of the cluster state, including the monitor map, manager map, the OSD map, the CRUSH map.  
	These maps are essential states that the OSD daemons uses to cordinate with each other. These monitors are also responsible for managing authentication between daemons and clients.
	At least three monitors are required for high availability and redundancy.

- __Ceph Managers__ 
	Ceph Manger daemons are responsible for keeping runtime metrics and the current state of the ceph cluster, including storage, perfomance and load utilizations metrics.
	Ceph manager daemons also host a python based modules to manager and expose ceph cluster information, including a web interface and a REST API
	At least 2 manager daemons are required for high availability.

- __Ceph MSD (MetaData Servers)__
	Ceph metadata servers store metadata on behalf of the ceph File System. It allows users to execute POSIX file system users to execute commands such as (ls, find) without overburdenning the cephFS


### Ceph architecture


