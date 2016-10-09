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
                           RUNNING/USED     PENDING/REQUESTED
                      -----------------     -----------------
            USERNAME   CPUS NODES  JOBS      CPUS NODES  JOBS
               user1    928    29     2         0     0     0
         	   user2     36     3     3         0     0     0
               user3   3008   102     3      1504    70     2
			   ...
                      -----------------     -----------------
               TOTAL  31926  1403  4362      9919   854  1401
           AVAILABLE  53472  2178 
```

## License

This project is in the worldwide public domain.  See [LICENSE](../LICENSE.md) for
more information.
