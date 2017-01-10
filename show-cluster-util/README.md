## show-cluster-util

**show-cluster-util** uses the Slurm Python bindings
([PySlurm](https://github.com/PySlurm/pyslurm)) to get all node information and
break it down by various states for the nodes as well as CPU and Memory.

## Dependencies

**show-cluster-util** requires the
[hostlist](https://www.nsc.liu.se/~kent/python-hostlist/) and
[PySlurm](https://github.com/PySlurm/pyslurm) Python modules.

## Configuration

Configuration is done by modifying the configuration section of the script.
There are three variables that can be adapted to the cluster setup:

- `EXCLUDED_PARTITIONS`: excluded partitions are not included in any output
- `PARTITION_GROUPS`: Nodes can be assigned to one (and only one) group depending
  on which partition they belong to. Output can be split up by group. See the script
  for more details
- `GRES`: Used to configure gres to to include in the output. A list of 2-element
  lists, each containing the name of a gres and the unit in which it is measured
  by slurm ("count", "MB", "GB", or "TB").


## Usage

`show-cluster-util` will report cluster utilization across all configured nodes
in all partitions.  Use the `-p` flag (once or multiple times) to specify a
partition and the (mutually exclusive) -g to split the output by node groups.

## Example Output
```
$ show-cluster-util

================================== All Nodes ===================================
  ALLOCATED |        IDLE |       MIXED |        DOWN |       TOTAL
  1240  40% |    952  31% |    624  20% |    274   9% |        3090
================================================================================

                cpu             mem             gpu        lscratch     
         ----------      ----------      ----------      ----------     
idle          34004  31%    76.7 TB  20%        107  79%   337.3 TB  27%
alloc         74038  67%   168.7 TB  43%         27  20%   196.3 TB  16%
unavail        2190   2%   147.6 TB  38%          2   1%   712.5 TB  57%
         ----------      ----------      ----------      ----------     
usable       110232        392.9 TB             136          1.2 PB     
down          11232         38.1 TB               8         96.3 TB     
         ----------      ----------      ----------      ----------     
total        121464        431.1 TB             144          1.3 PB     

```

The states are defined as follows:

| State | Description |
| ----- | ----------- |
| Allocated | Resources that have been requested and allocated by user jobs |
| Idle | Resources that are not allocated and available to newly submitted jobs | 
| Down | Resources that belong to nodes that are in the DOWN or DRAINED states |
| Unavailable | Resources that are unused but not available to newly submitted jobs due the way jobs have allocated resources on the node |
| Usable | Resouces that belong to nodes not in the DOWN or DRAINED states |
| Total | All resouces regardless of state |

## License

This project is in the worldwide public domain.  See [LICENSE](../LICENSE.md) for
more information.
