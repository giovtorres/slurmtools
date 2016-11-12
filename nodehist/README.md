## nodehist

Similar to
[userhist](https://github.com/giovtorres/slurmtools/tree/master/userhist),
*nodehist* queries Elasticsearch for all running and completed jobs on a
particular node. It is faster and more lightweight than using sacct to query
past jobs.

## Dependencies

* [PySlurm](https://github.com/PySlurm/pyslurm)
* [noded](https://github.com/giovtorres/noded)
* [Python Elasticsearch
  Client](https://elasticsearch-py.readthedocs.io/en/master/)
* [Slurm Elasticsearch Job Completion
  plugin](https://github.com/asanchez1987/jobcomp-elasticsearch/blob/master/INSTALL.md)


## Usage

```
usage: nodehist [-h] [-t LAST] node

Return a list of current and past jobs on a given node.

positional arguments:
  node        node to query

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


## License

This project is in the worldwide public domain.  See [LICENSE](../LICENSE.md) for
more information.
