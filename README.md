Hari Sekhon - DevOps Bash Tools
===============================

[![Build Status](https://travis-ci.org/HariSekhon/DevOps-Bash-tools.svg?branch=master)](https://travis-ci.org/HariSekhon/DevOps-Bash-tools)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/c61193dd7dcc418b85149bddf93362e4)](https://www.codacy.com/app/harisekhon/bash-tools)
[![Platform](https://img.shields.io/badge/platform-Linux%20%7C%20OS%20X-blue.svg)](https://github.com/harisekhon/bash-tools#hari-sekhon---bash-tools)
[![DockerHub](https://img.shields.io/badge/docker-available-blue.svg)](https://hub.docker.com/r/harisekhon/centos-github/)

100+ Shell Scripts, Advanced Bash environment & Utility Code Library used by all my other [GitHub repos](https://github.com/harisekhon) CI builds.

Contains:

- Systems Administation scripts - scripts to make systems administration faster and easier for common tasks, including wrappers to common commands that auto-populate required switches
- Scripts for CI builds across all my other repos, forming a drop-in framework containing many common checks
- Bash environment enhancements - advanced `.bashrc` + `.bash.d/*.sh`, advanced configuration files for common tools like [vim](https://www.vim.org/), [screen](https://www.gnu.org/software/screen/), [tmux](https://github.com/tmux/tmux/wiki), installs the best sysadmin packages like those above plus [AWS CLI](https://aws.amazon.com/cli/), [jq](https://stedolan.github.io/jq/) and many others, adds dynamic [git](https://git-scm.com/) and shell behaviour enhancements, colouring, functions, aliases and automatic pathing of many common installation locations for many major languages like Python, Perl, Ruby, NodeJS...
- Utility library used in many scripts here and sourced from other repos, using the 2 libraries
  - `.bash.d` - interactive library (huge)
  - `lib` - script library

For more advanced Systems Administration scripts in other languages, see the repos listed at the bottom of the page.

These scripts can be used straight from the git clone, but see setup benefits of `make install` next.

### Quick Setup

```
make install
```

- Adds sourcing to `.bashrc`/`.bash_profile` to automatically inherit all `.bash.d/*.sh` environment enhancements for all technologies (see [Inventory Overview](https://github.com/harisekhon/devops-bash-tools#Inventory-Overview) below)
- Symlinks all `.*` config files to `$HOME` for [git](https://git-scm.com/), [vim](https://www.vim.org/), top, [htop](https://hisham.hm/htop/), [screen](https://www.gnu.org/software/screen/), [tmux](https://github.com/tmux/tmux/wiki), [editorconfig](https://editorconfig.org/), [Ansible](https://www.ansible.com/) etc.
- Installs OS package dependencies for all scripts (detects the OS and installs the right RPMs, Debs, Apk or Mac HomeBrew packages)
- Installs Python packages including [AWS CLI](https://aws.amazon.com/cli/)

`make install` effectively does `make system-packages bash python aws`, but if you want to pick and choose from different sections, see [Individual Setup Parts](https://github.com/harisekhon/devops-bash-tools#Individual-Setup-Parts) below.

### Inventory Overview

- Scripts - [Linux](https://en.wikipedia.org/wiki/Linux) / [Mac](https://en.wikipedia.org/wiki/MacOS) systems administration scripts:
  - installation scripts for various OS packages (RPM, Deb, Apk) for various Linux distros ([Redhat RHEL](https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux) / [CentOS](https://www.centos.org/) / [Fedora](https://getfedora.org/), [Debian](https://www.debian.org/) / [Ubuntu](https://ubuntu.com/), [Alpine](https://alpinelinux.org/))
  - install if absent scripts for Python, Perl, Ruby, NodeJS and Golang packages - good for minimizing the number of source code installs by first running the OS install scripts and then only building modules which aren't already detected as installed (provided by system packages), speeding up builds and reducing the likelihood of compile failures
  - install scripts for [Jython](https://www.jython.org/) and build tools like [Gradle](https://gradle.org/) and [SBT](https://www.scala-sbt.org/) for when Linux distros don't provide packaged versions or where the packaged versions are too old
  - Git branch management
  - utility scripts used from other scripts
- `.*` - dot conf files for lots of common software eg. advanced `.vimrc`, `.gitconfig`, massive `.gitignore`, `.editorconfig`, `.screenrc`, `.tmux.conf` etc.
  - `.vimrc` - contains many awesome [vim](https://www.vim.org/) tweaks, plus hotkeys for linting lots of different file types in place, including Python, Perl, Bash / Shell, Dockerfiles, JSON, YAML, XML, CSV, INI / Properties files, LDAP LDIF etc without leaving the editor!
  - `.screenrc` - fancy [screen](https://www.gnu.org/software/screen/) configuration including advanced colour bar, large history, hotkey reloading, auto-blanking etc.
  - `.tmux.conf` - fancy [tmux](https://github.com/tmux/tmux/wiki) configuration include advanced colour bar and plugins, settings, hotkey reloading etc.
  - [Git](https://git-scm.com/):
    - `.gitconfig` - advanced Git configuration
    - `.gitignore` - extensive Git ignore of trivial files you shouldn't commit
    - enhanced Git diffs
    - protections against committing AWS access keys & secrets keys, merge conflict unresolved files
- `.bashrc` - shell tuning and sourcing of `.bash.d/*.sh`
- `.bash.d/*.sh` - thousands of lines of advanced bashrc code, aliases, functions and environment variables for:
  - [Linux](https://en.wikipedia.org/wiki/Linux) & [Mac](https://en.wikipedia.org/wiki/MacOS)
  - SCM - [Git](https://git-scm.com/), [Mercurial](https://www.mercurial-scm.org/), [Svn](https://subversion.apache.org)
  - [AWS](https://aws.amazon.com/)
  - [Docker](https://www.docker.com/)
  - [Kubernetes](https://kubernetes.io/)
  - [Kafka](http://kafka.apache.org/)
  - [Vagrant](https://www.vagrantup.com/)
  - automatic GPG and SSH agent handling for handling encrypted private keys without re-entering passwords, and lazy evaluation to only prompt key load the first time SSH is called
  - and lots more - see [.bash.d/README](https://github.com/HariSekhon/DevOps-Bash-tools/blob/master/.bash.d/README.md) for a more detailed list
  - run `make bash` to link `.bashrc`/`.bash_profile` and the `.*` dot config files to your `$HOME` directory to auto-inherit everything
- `lib/*.sh` - Bash utility libraries full of functions for [Docker](https://www.docker.com/), environment, CI detection ([Travis CI](https://travis-ci.org/), [Jenkins](https://jenkins.io/)), port and HTTP url availability content checks etc. Sourced from all my other [GitHub repos](https://github.com/harisekhon) to make setting up Dockerized tests easier.
- `setup/install_*.sh` - various simple to use installation scripts for common technologies like [Ansible](https://www.ansible.com/), [Terraform](https://www.terraform.io/), [MiniKube](https://kubernetes.io/docs/setup/learning-environment/minikube/) and [MiniShift](https://www.okd.io/minishift/) (Kubernetes / [Redhat OpenShift](https://www.openshift.com/)/[OKD](https://www.okd.io/) dev VMs), [Maven](https://maven.apache.org/), [Gradle](https://gradle.org/), [SBT](https://www.scala-sbt.org/), [EPEL](https://fedoraproject.org/wiki/EPEL), [RPMforge](http://repoforge.org/), [Homebrew](https://brew.sh/), [Travis CI](https://travis-ci.org/), [Parquet Tools](https://github.com/apache/parquet-mr/tree/master/parquet-tools) etc.
- `kafka_wrappers/*.sh` - scripts to make [Kafka](http://kafka.apache.org/) CLI usage easier including auto-setting Kerberos to source TGT from environment and auto-populating broker and zookeeper addresses. These are auto-added to the `$PATH` when `.bashrc` is sourced. For something similar for [Solr](https://lucene.apache.org/solr/), see `solr_cli.pl` in the [DevOps Perl Tools](https://github.com/harisekhon/devops-perl-tools) repo.
- `curl_auth.sh` - wraps curl to send username/password through a ram file descriptor to avoid arguments where the credentials can be logged
- `k8s_api.sh` - finds Kubernetes API and runs your curl arguments against it, auto-getting authorization token and populating Authorization: Bearer header
- `ldapsearch.sh` - wraps ldapsearch to infer most of the settings for you and use environment variables for overrides
- `ldap_user_recurse.sh` / `ldap_group_recurse.sh` - recurse Active Directory LDAP users upwards to find all parents groups, or groups downwards to find all nested users (useful for debugging LDAP integration and group-based permissions)
- `zookeeper-client.sh` - wraps zookeeper-client, auto-finds the zookeeper quorum from /etc to make it faster and easier to connect
- `beeline.sh` - connects to [HiveServer2](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Overview) via beeline, auto-populating Kerberos and SSL settings, and using `$HIVESERVER_HOST` environment variable so you can connect with no arguments (prompts for HiveServer2 address if you haven't set this environment variable)
- `beeline_zk.sh` - connects to [HiveServer2](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Overview) HA via beeline, auto-populating SSL and ZooKeeperi service discovery settings (use specify `$ZOOKEEPERS` environment variable)
- `impala_shell.sh` - connects to a random [Impala](https://impala.apache.org/) node via impala-shell, parsing the Hadoop topology map and selecting a random datanode to connect to Impalad. Can specify explicit `$IMPALA_HOST` environment variable override and also enable SSL via `IMPALA_SSL=1` environment or `--ssl` switch as per normal
- `hdfs_checksum*.sh` - walks an HDFS directory tree and outputs HDFS native checksums, MD5-of-MD5 or the portable externally comparable CRC32, in serial or in parallel
- `hdfs_find_replication_factor_1.sh` / `hdfs_set_replication_factor_3.sh` - finds HDFS files with replication factor 1 / sets HDFS files with replication factor <=2 to replication factor 3 to repair replication safety and avoid no replica alarms during maintenance operations (see a faster Python version in the [DevOps Python Tools](https://github.com/harisekhon/devops-python-tools) repo)
- `hdfs_file_size.sh` / `hdfs_file_size_including_replicas.sh` - quickly differentiate HDFS files raw size vs 3x replicated size
- `cloudera_manager_impala_queries.sh` - queries [Cloudera Manager](https://www.cloudera.com/products/product-components/cloudera-manager.html) for recent [Impala](https://impala.apache.org/) queries
- `aws*.sh` - various [AWS](https://aws.amazon.com/) day-to-day scripts for EC2 metadata, Spot Termination, SSM Parameter Store secret put from prompt, IAM Credential Reports on IAM users without MFA, old access keys and passwords, old users that haven't logged in or used an access key recently etc.
- `gce*.sh` - [Google Cloud](https://cloud.google.com/) Compute Engine scripts for metadata API and pre-emption
- `check_*.sh` - extensive collection of generalized tests that can be applied to any repo and run against all my GitHub repos via CI
- `git*.sh` - various useful Git scripts like iterating all branches executing command arguments, submodule handling, merging master updates to all branches, fetching GitHub users public SSH keys for quick local installation etc.

- Programming language linting:

  - [Python](https://www.python.org/) (syntax, pep8, pre-byte-compiling)
  - [Perl](https://www.perl.org/)
  - [Java](https://www.java.com/en/)
  - [Scala](https://www.scala-lang.org/)
  - [Ruby](https://www.ruby-lang.org/en/)
  - [Bash](https://www.gnu.org/software/bash/) / Shell
  - Misc (whitespace, custom enforced checks like not calling `quit()` in Python programs etc.)

- Build System & CI linting:

  - [Make](https://www.gnu.org/software/make/)
  - [Maven](https://maven.apache.org/)
  - [SBT](https://www.scala-sbt.org/)
  - [Gradle](https://gradle.org/)
  - [Travis CI](https://travis-ci.org/)

- Data format validation using programs from my [DevOps Python Tools repo](https://github.com/harisekhon/devops-python-tools):

  - CSV
  - JSON
  - [Avro](https://avro.apache.org/)
  - [Parquet](https://parquet.apache.org/)
  - INI / Properties files (Java)
  - LDAP LDIF
  - XML
  - YAML

Currently utilized in the following GitHub repos:

* [DevOps Python Tools](https://github.com/harisekhon/devops-python-tools) - 75+ DevOps CLI tools for Hadoop, HBase, Spark, Log Anonymizer, Ambari Blueprints, AWS CloudFormation, Linux, Docker, Spark Data Converters & Validators (Avro / Parquet / JSON / CSV / INI / XML / YAML), Elasticsearch, Solr, Travis CI, Pig, IPython

* [DevOps Perl Tools](https://github.com/harisekhon/perl-tools) - 25+ DevOps CLI tools for Hadoop, HDFS, Hive, Solr/SolrCloud CLI, Log Anonymizer, Nginx stats & HTTP(S) URL watchers for load balanced web farms, Dockerfiles & SQL ReCaser (Hive, Impala, MySQL, PostgreSQL, Cassandra CQL, Apache Drill, Couchbase N1QL, Microsoft SQL Server, Oracle, Pig Latin, Neo4j, InfluxDB), Ambari FreeIPA Kerberos, Datameer, Linux...

* [The Advanced Nagios Plugins Collection](https://github.com/harisekhon/nagios-plugins) - 450+ programs for Hadoop, Docker, Kafka, Elasticsearch, RabbitMQ, Redis, HBase, Solr, Cassandra, ZooKeeper, HDFS, Yarn, Hive, Presto, Drill, Impala, Consul, Spark, Jenkins, Travis CI, Git, MySQL, Linux, DNS, Whois, SSL Certs, Yum Security Updates, Kubernetes, Mesos, Riak, MongoDB, Memcached, Couchbase, CouchDB, Neo4j, Ambari, Cloudera, Hortonworks, MapR etc.

* [HAProxy-configs](https://github.com/harisekhon/haproxy-configs) - 80+ HAProxy Configs for Hadoop, Big Data, NoSQL, Docker, Elasticsearch, SolrCloud, HBase, Cloudera, Hortonworks, MapR, MySQL, PostgreSQL, Apache Drill, Hive, Presto, Impala, ZooKeeper, OpenTSDB, InfluxDB, Prometheus, Kibana, Graphite, SSH, RabbitMQ, Redis, Riak, Rancher etc.

* [Dockerfiles](https://github.com/HariSekhon/Dockerfiles) - 50+ DockerHub public images for Docker & Kubernetes - Hadoop, Kafka, ZooKeeper, HBase, Cassandra, Solr, SolrCloud, Presto, Apache Drill, Nifi, Spark, Mesos, Consul, Riak, OpenTSDB, Jython, Advanced Nagios Plugins & DevOps Tools repos on Alpine, CentOS, Debian, Fedora, Ubuntu, Superset, H2O, Serf, Alluxio / Tachyon, FakeS3

* [Perl Lib](https://github.com/harisekhon/lib) - Perl utility library
* [PyLib](https://github.com/harisekhon/pylib) - Python utility library
* [Lib-Java](https://github.com/harisekhon/lib-java) - Java utility library
* [Nagios Plugin Kafka](https://github.com/harisekhon/nagios-plugin-kafka) - Kafka Nagios Plugin written in Scala with Kerberos support

[Pre-built Docker images](https://hub.docker.com/u/harisekhon/) are available for those repos (which include this one as a submodule) and the ["docker available"](https://hub.docker.com/r/harisekhon/centos-github/)  icon above links to an [uber image](https://hub.docker.com/r/harisekhon/centos-github/) which contains all my github repos pre-built. There are [Centos](https://hub.docker.com/r/harisekhon/centos-github/), [Alpine](https://hub.docker.com/r/harisekhon/alpine-github/), [Debian](https://hub.docker.com/r/harisekhon/debian-github/) and [Ubuntu](https://hub.docker.com/r/harisekhon/ubuntu-github/) versions of this uber Docker image containing all repos.

#### Individual Setup Parts

Optional, only if you don't do the full `make install`.

Install only OS system package dependencies and [AWS CLI](https://aws.amazon.com/cli/) via Python Pip (doesn't symlink anything to `$HOME`):

```
make
```

Adds sourcing to `.bashrc` and `.bash_profile` and symlinks dot config files to `$HOME` (doesn't install OS system package dependencies):

```
make link
```

undo via

```
make unlink
```

Install only OS system package dependencies (doesn't include [AWS CLI](https://aws.amazon.com/cli/) or Python packages):

```
make system-packages
```

Install [AWS CLI](https://aws.amazon.com/cli/):

```
make aws
```

Install generically useful Python CLI tools and modules (includes [AWS CLI](https://aws.amazon.com/cli/), autopep8 etc):

```
make python
```

### Stargazers over time

[![Stargazers over time](https://starchart.cc/HariSekhon/DevOps-Bash-tools.svg)](https://starchart.cc/HariSekhon/DevOps-Bash-tools)
