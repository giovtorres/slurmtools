## salljobs

**salljobs** (show all jobs) reports CPU, Node, Job, and Job State usage
summaries for each user on the cluster.

## Dependencies

[PySlurm](https://github.com/PySlurm/pyslurm) is required.


## Usage

Default output shows all users. Use the `-p` flag without any arguments to show
all users by partitions.

* Use the `-h` flag for help.
* Use the `-u` flag for specifying one or more users (space separated)
* Use the `-p` flag for specifying one or more partitions (space separated)

You may use both `-u` and `-p` together to filter for user(s) in certain
partition(s).


## Example

```
                             RUNNING                PENDING    
                     -----------------------    ---------------
            USERNAME    CPUS   NODES    JOBS       CPUS    JOBS
               user1    1120      20       2          0       0
               user2     288       9       9          0       0
               user3    3194      81      26        100       1
               [...]
                     -----------------------    ---------------
               TOTAL   72000    1808   10706      30380    1170
           AVAILABLE  108840    2789                           

The number of CPUs for PENDING jobs is a minimal estimate.
Actual allocation may be different.
```

## License

This project is in the worldwide public domain.  See [LICENSE](../LICENSE.md) for
more information.
