## userhist

**userhist** queries Elasticsearch for a user's completed jobs.  It is faster
and more lightweight than using `sacct` to query past jobs.

## Dependencies

The following Python module and Slurm plugin are required:

* [Python Elasticsearch
  Client](https://elasticsearch-py.readthedocs.io/en/master/)
* [Slurm Elasticsearch Job Completion
  plugin](https://github.com/asanchez1987/jobcomp-elasticsearch/blob/master/INSTALL.md)


## Usage

```
usage: userhist [-h] [-t LAST] user

Return a list of past jobs for a given user.

positional arguments:
  user        user to query

optional arguments:
  -h, --help  show this help message and exit
  -t LAST     specify time range (default=2h)

    Example time ranges:
        2h  = last 2 hours (default)
        12h = last 12 hours
        3d  = last 3 days
        2w  = last 2 weeks
```

## Example

```
-------------- Jobs ended in the last 48h for user1 --------------
         JOBID             USER   PARTITION CPUS            STARTTIME              ENDTIME      STATE NODELIST
       4815610            user1        norm   32  2016-10-08 05:31:27  2016-10-08 20:21:45  COMPLETED cn0799
       4815565            user1        norm   32  2016-10-08 04:49:03  2016-10-09 04:49:15    TIMEOUT cn0882
```

## License

This project is in the worldwide public domain.  See [LICENSE](../LICENSE.md) for
more information.
