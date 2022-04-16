# legos

Legos is an `asset management system` designed to be modular, flexible and easily extensible.


## Native Database

Initially [Neo4J](https://neo4j.com/) was used as the native database for `legos`, however since the community edition of `Neo4J` is not available for use in cluster/cloud setups, I have decided to look at alternatives which **do** support cluster deployment. As of this writing, I have decided to go agead with [Redis](https://redis.io/). However, `Neo4J` is still part of 2 extentions of `legos` which is positioned for a more data analytics role named `overwatch` and `clairvoyance`.

A very minimal DB is maintained and can be swapped with a studio's own DB layer.


## NOTE

| Tables | UID       | VERSIONS    |
|--------|-----------|-------------|
| Fields | path      | version num |
|        | name      |             |
|        | type      |             |
|        | timestamp |             |
|        | status    |             |
|        | version   |             |


### Examples

```text

uid:df506871f17e461ea2bf6a3c6e914a74 path /path/to/some/asset.json
uid:df506871f17e461ea2bf6a3c6e914a74 name some_asset
uid:df506871f17e461ea2bf6a3c6e914a74 type LookDevPackage
uid:df506871f17e461ea2bf6a3c6e914a74 timestamp '2020-12-04 22:49:30.855034'
uid:df506871f17e461ea2bf6a3c6e914a74 status APPROVED
```

version|                              sha                              |      version num       |        asset/entity uid
version:adbc0049a2f4478ec06a25bb526a295ab3551a31d6eb789c7c488b8c46eaa3cf         1              df506871f17e461ea2bf6a3c6e914a74

The redis queries would then look like:

```shell

HSET uid:df506871f17e461ea2bf6a3c6e914a74 path /jobs_sandbox/FOO/packages/skaarj/skaarj_assetprep/ldev/lookdevpackage/skaarj/0001/skaarj.json
HSET version:adbc0049a2f4478ec06a25bb526a295ab3551a31d6eb789c7c488b8c46eaa3cf 1 df506871f17e461ea2bf6a3c6e914a74
HLEN version:adbc0049a2f4478ec06a25bb526a295ab3551a31d6eb789c7c488b8c46eaa3cf
HGET version:adbc0049a2f4478ec06a25bb526a295ab3551a31d6eb789c7c488b8c46eaa3cf 2
HSET version:adbc0049a2f4478ec06a25bb526a295ab3551a31d6eb789c7c488b8c46eaa3cf 2 df506871f17e461ea2bf6a3c6e914a74
HSET uid:df506871f17e461ea2bf6a3c6e914a74 name skaarj
```


From Python, we can query redis as shown below:

```python

import redis

r = redis.Redis(decode_responses=True, host='127.0.0.1', port='6379')
# Manually specify IP and port for connection
# r = redis.from_url('redis://127.0.0.1:6379')
r.hget('uid:df506871f17e461ea2bf6a3c6e914a74', 'name')
r.hgetall('version:adbc0049a2f4478ec06a25bb526a295ab3551a31d6eb789c7c488b8c46eaa3cf')
r.hlen('version:adbc0049a2f4478ec06a25bb526a295ab3551a31d6eb789c7c488b8c46eaa3cf')
r.hget('version:adbc0049a2f4478ec06a25bb526a295ab3551a31d6eb789c7c488b8c46eaa3cf', 1)

r.hset('uid:80476b84a95746f2a452428252cd15ec', 'name', 'skaarj_look_assignments')
```


## Resources

* [Python Examples](https://pythontic.com/database/redis/list)
