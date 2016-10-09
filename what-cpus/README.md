## what-cpus

The **what-cpus** script prints process and thread information for all Slurm
jobs running on a compute node.  

## Dependencies

[psutil](https://github.com/giampaolo/psutil) is required.


## Example

```
JobID : 24406544 (#1)
User  : user1
CPU Affinity (1 core)
   \_ cores       |  3| 
   \_ hypercores  | 11| 

   PID:  24620 (slurm_script)                                      [3,11]
     \_ TID: 24620   State: S   Processor: 11   RSS:   1.6 MB      [3,11]
   PID:  24827 (bash)                                              [3,11]
     \_ TID: 24827   State: S   Processor: 11   RSS:   1.5 MB      [3,11]
   PID:  24838 (R)                                                 [3,11]
     \_ TID: 24838   State: R   Processor: 11   RSS: 448.7 MB      [3,11]
Job Summary: 1 running thread(s) / 3 total threads
             1 core(s), using 451.8 MB of RAM

JobID : 24552520 (#2)
User  : user2
CPU Affinity (1 core)
   \_ cores       |  5| 
   \_ hypercores  | 13| 

   PID:    300 (slurm_script)                                      [5,13]
     \_ TID:   300   State: S   Processor: 13   RSS:   1.6 MB      [5,13]
   PID:    354 (bash)                                              [5,13]
     \_ TID:   354   State: S   Processor:  5   RSS:   1.5 MB      [5,13]
   PID:    358 (R)                                                 [5,13]
     \_ TID:   358   State: R   Processor:  5   RSS: 443.2 MB      [5,13]
Job Summary: 1 running thread(s) / 3 total threads
             1 core(s), using 446.3 MB of RAM


Node Summary:
  Number of Jobs : 2
  Number of Users: 2
  User List      : user1 user2 

System Info:
  CPU   : 13.80%
  Load  : 2.00 2.05 2.38
  Memory: 8.70%
  Swap  : 0.00%
```

## How It Works

**what-cpus** does the following:

1. Find if there are any slurm jobs running on the node
2. If there are jobs running, print the jobid and the allocated CPUs
3. For each job, print all process IDs 
4. For each process, print the thread ID, its state, last run processor, RSS usage and CPU allocation.

Since a thread is the smallest unit of execution, a single-threaded process will 
run one thread and the IDs of both the process and thread will be the same.

The above example shows an MPI job.  It is allocated all cores on the node and
even though each process is pinned to a core, it appears each process is
multithreaded.  Furthermore, only one of those thread pairs is in the RUNNING
state at any given time, which seems correct for a properly submitted MPI job.

CPUS 0-15 are cores and CPUS 16-31 are the respective hyperthreads.  For 
example, CPU0 is the core CPU and CPU16 is its hyperthread, and so on.

## License

This project is in the worldwide public domain.  See [LICENSE](../LICENSE.md) for
more information.
