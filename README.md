Redis
========
[![Galaxy](https://img.shields.io/badge/galaxy-samdoran.redis-blue.svg?style=flat)](https://galaxy.ansible.com/samdoran/redis)

Install [redis](http://redis.io), an in-memory data structure store, on RHEL 6/7.

Requirements
------------

None.

Role Variables
--------------

| Name              | Default Value       | Description          |
|-------------------|---------------------|----------------------|
| `redis_major_version` | `2` | Major version of `redis` to install. Version 2 comes from `epel`, version 3 comes from `remi`. Changing this variable changes the repository enabled during installation. |
| `redis_max_open_files` | `65536` | Sets the `ulimit` value for the `redis` user. |

All variables in the `redis.conf` file are available to the role. They are defined, along with comments from the original `redis.conf`, in `defaults/main.yml`. The `redis.conf.j2` tempalate will insert different settings based on the version of `redis` running on the target host.

Dependencies
------------

- samdoran.repo-epel (for `redis` 2.x)
- samdoran.repo-remi (for `redis` 3.x)

Example Playbook
-------------------------

    - hosts: redis
      roles:
        - { role: samdoran.repo-epel, when: redis_major_version == 2 }
        - { role: samdoran.repo-remi, when: redis_major_version == 3 }
        - redis

License
-------

MIT
