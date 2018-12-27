---
title: Setup Mongodb 3.6 on Amazon Linux
categories: Web Developer Bootcamp
date: Sun Jun 10 17:19:31 2018
tags:
- front end
---

Recently I'm learning how to use AWS Cloud9 and found many tutorials were too old to fit the current Amazon Linux.

### Create the .repo file

Because `mongodb-org` cannot be directly installed any more on Amazon Linux, we need to create the repository file by

```bash
sudo vi /etc/yum.repos.d/mongodb-org-3.6.repo
```

Then add the following content to the .repo file

```
[mongodb-org-3.6]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/amazon/2013.03/mongodb-org/3.6/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.6.asc
```

### Install the MongoDB package

```bash
sudo yum install -y mongodb-org
```

If you see any error saying any conflict with MongoDB of older versions, use `yum remove` to uninstall the older version and retry the install command.

### Run MongoDB on Amazon Linux

Almost use the same commands with this [post](https://community.c9.io/t/setting-up-mongodb/1717), except:

- Remove `--rest "$@"` because the `--rest` parameter was removed in MongoDB 3.6 introduced by this [article](https://docs.mongodb.com/manual/core/security-mongodb-configuration/).



