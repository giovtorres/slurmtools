## show-cluster-util

**show-cluster-util** uses the Slurm Python bindings
([PySlurm](https://github.com/PySlurm/pyslurm)) to get all node information and
break it down by various states for the nodes as well as CPU and Memory.

## Dependencies

**show-cluster-util** requires the
[hostlist](https://www.nsc.liu.se/~kent/python-hostlist/) and
[PySlurm](https://github.com/PySlurm/pyslurm) Python modules.

## Example Output
```
$ show-cluster-util

Total Allocated Nodes             :      858
Total Mixed Nodes                 :      526
Total Idle Nodes                  :      490
Total Down/Offline Nodes          :      251
Total Eligible Nodes              :     1874
Total Configured Nodes            :     2125

Total Allocated CPUs              :    31060
Total Idle CPUs                   :    15628
Total Down CPUs                   :     5596
Total Unallocatable CPUs          :     1220
Total Eligible CPUs               :    47908
Total Configured CPUs             :    53504
Cluster CPU % Unallocatable       :       2%
Cluster CPU % (Alloc + Unalloc)   :      67%

Total Allocated Memory            :  60.7 TB
Total Idle Memory                 :  25.0 TB
Total Down Memory                 :   7.6 TB
Total Unallocatable Memory        :  40.6 TB
Total Overallocated Memory        :  14.3 GB
Total Eligible Memory             : 126.4 TB
Total Configured Memory           : 134.0 TB
Cluster Memory % Unallocatable    :      32%
Cluster Memory % (Alloc + Unalloc):      80%

```

For CPUs and or Memory, the various states are defined as follows:

| State | Description |
| ----- | ----------- |
| Allocated | CPUs or Memory that have been requested and allocated by user jobs |
| Idle | CPUs or Memory that are not allocated and available to newly submitted jobs | 
| Down/Offline | CPUs or Memory that belong to nodes that are in the DOWN or DRAINED states |
| Unallocatable | CPUs or Memory that are unused but not available to newly submitted jobs due the way jobs have allocated resources on the node |
| Overallocated | Memory that Slurm has overallocated to one or more jobs on a node.  In this case, allocated memory on the node is greater than the configured real memory |
| Eligible | CPUs or Memory that belong to nodes not in the DOWN or DRAINED states |
| Configured | CPUs or Memory that belong to all nodes regardless of state |

## License

This project is in the worldwide public domain.  See [LICENSE](LICENSE.md) for
more information.
