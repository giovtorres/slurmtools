## show-cluster-util

**show-cluster-util** uses the Slurm Python bindings
([PySlurm](https://github.com/PySlurm/pyslurm)) to get all node information and
break it down by various states for the nodes as well as CPU and Memory.

## Dependencies

**show-cluster-util** requires the
[hostlist](https://www.nsc.liu.se/~kent/python-hostlist/) and
[PySlurm](https://github.com/PySlurm/pyslurm) Python modules.

## Configuration

If you have purely floating partitions, they should be configured in the
`FLOATING_PARTITIONS` list. Partitions that should be ignored should be
added to the `IGNORED_PARTITIONS` list.

Nodes that are only in ignored partitions are not included in the
results. Nodes that are only in floating partitions are included, but
a warning will be displayed when running with `-v`.

In addtion groups of partitions can be configured in a nested list
called `PARTITION_GROUPS` and GRESes are defined in `GRES`.

The script sets the path to the pyslurm package manually. This will
have to be configured as well.

## Usage

`show-cluster-util` will report cluster utilization across all configured
nodes in all partitions.  Use the `-p` flag to specify a partition. Use the
`-g` flag to show the utilization by group.

```
$ show-cluster-util

============================= All Nodes (N = 4208) =============================
  ALLOCATED |       IDLE |      MIXED |   RESERVED |       DOWN |      MAINT
  2165  51% |   517  12% |  1333  32% |     0   0% |   109   3% |    84   2%
================================================================================

                cpu             mem             gpu        lscratch     
         ----------      ----------      ----------      ----------     
idle          47490  25%   110.5 TB  14%        143  23%   570.1 TB  24%
alloc        142340  74%   432.0 TB  56%        467  76%   418.0 TB  17%
unavail        1754   1%   231.8 TB  30%          2   0%     1.4 PB  59%
         ----------      ----------      ----------      ----------     
usable       191584        774.3 TB             612          2.4 PB     
down           3752         11.7 TB              38         32.7 TB     
maint          4320         18.3 TB               0         39.1 TB     
         ----------      ----------      ----------      ----------     
total        195336        786.0 TB             650          2.4 PB     

$ show-cluster-util -v


============================= All Nodes (N = 4208) =============================
  ALLOCATED |       IDLE |      MIXED |   RESERVED |       DOWN |      MAINT
  2156  51% |   518  12% |  1341  32% |     0   0% |   109   3% |    84   2%
================================================================================

                cpu             mem             gpu        lscratch     
         ----------      ----------      ----------      ----------     
idle          47764  25%   112.3 TB  15%        143  23%   576.7 TB  24%
alloc        142138  74%   430.7 TB  56%        467  76%   416.8 TB  17%
unavail        1682   1%   231.2 TB  30%          2   0%     1.4 PB  59%
         ----------      ----------      ----------      ----------     
usable       191584        774.3 TB             612          2.4 PB     
down           3752         11.7 TB              38         32.7 TB     
maint          4320         18.3 TB               0         39.1 TB     
         ----------      ----------      ----------      ----------     
total        195336        786.0 TB             650          2.4 PB     


=================================== Warnings ===================================
- Node cn0625 (fnord) is only part of ignored partitions; not included
- Node cn0624 (fnord) is only part of ignored partitions; not included
- Node cn0623 (fnord) is only part of ignored partitions; not included


$ show-cluster-util -p norm


============================ norm Nodes (N = 1567) =============================
  ALLOCATED |       IDLE |      MIXED |   RESERVED |       DOWN |      MAINT
   705  45% |     0   0% |   797  51% |     0   0% |    13   1% |    52   3%
================================================================================

                cpu             mem             gpu        lscratch     
         ----------      ----------      ----------      ----------     
idle          11162  15%    30.6 TB  10%          0   0%   207.2 TB  21%
alloc         60116  83%   232.6 TB  76%          0   0%   275.5 TB  28%
unavail        1530   2%    41.9 TB  14%          0   0%   497.8 TB  51%
         ----------      ----------      ----------      ----------     
usable        72808        305.1 TB               0        980.5 TB     
down            704          3.0 TB               0          6.6 TB     
maint          2528         10.6 TB               0         26.6 TB     
         ----------      ----------      ----------      ----------     
total         73512        308.1 TB               0        987.1 TB     
```


For CPUs and or Memory, the various states are defined as follows:

| State | Description |
| ----- | ----------- |
| Allocated | CPUs or Memory that have been requested and allocated by user jobs |
| Idle | CPUs or Memory that are not allocated and available to newly submitted jobs | 
| Down | CPUs or Memory that belong to nodes that are in the DOWN or DRAINED states |
| Maint| Under maintenance|
| Unavailable | CPUs or Memory that are unused but not available to newly submitted jobs due the way jobs have allocated resources on the node |
| Overallocated | Memory that Slurm has overallocated to one or more jobs on a node.  In this case, allocated memory on the node is greater than the configured real memory |
| Usable | CPUs or Memory that belong to nodes not in the DOWN or DRAINED states |
| Total | CPUs or Memory that belong to all nodes regardless of state |
