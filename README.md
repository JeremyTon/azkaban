# Azkaban 

[![Build Status](https://travis-ci.com/azkaban/azkaban.svg?branch=master)](https://travis-ci.com/azkaban/azkaban)[![codecov.io](https://codecov.io/github/azkaban/azkaban/branch/master/graph/badge.svg)](https://codecov.io/github/azkaban/azkaban)[![Join the chat at https://gitter.im/azkaban-workflow-engine/Lobby](https://badges.gitter.im/azkaban-workflow-engine/Lobby.svg)](https://gitter.im/azkaban-workflow-engine/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)[![Documentation Status](https://readthedocs.org/projects/azkaban/badge/?version=latest)](http://azkaban.readthedocs.org/en/latest/?badge=latest)


## Build
Azkaban builds use Gradle and requires Java 8 or higher.

The following set of commands run on *nix platforms like Linux, OS X.

```
# Build Azkaban
./gradlew build

# Clean the build
./gradlew clean

# Build and install distributions
./gradlew installDist

# Run tests
./gradlew test

# Build without running tests
./gradlew build -x test
```

### Build a release

Pick a release from [the release page](https://github.com/azkaban/azkaban/releases). 
Find the tag corresponding to the release.

Check out the source code corresponding to that tag.
e.g.

`
git checkout 3.30.1
`

Build 
```
./gradlew clean build
```

## Documentation

The current documentation will be deprecated soon at [azkaban.github.io](http://azkaban.github.io). 
The [new Documentation site](https://azkaban.readthedocs.io/en/latest/) is under development.
The source code for the documentation is inside `docs` directory.

For help, please visit the [Azkaban Google Group](https://groups.google.com/forum/?fromgroups#!forum/azkaban-dev).

## Developer Guide

See [the contribution guide](https://github.com/azkaban/azkaban/blob/master/CONTRIBUTING.md).

#### Documentation development

If you want to contribute to the documentation or the release tool (inside the `tools` folder), 
please make sure python3 is installed in your environment. python virtual environment is recommended to run these scripts.

To create a venv & install the python3 dependencies inside it, run

```bash
python3 -m venv venv
source venv/bin/activate
pip3 install -r requirements.txt
```
After, enter the documentation folder `docs` and make the build by running
```bash
cd docs
make html
```

Find the built docs under `_build/html/`.

For example on a Mac, open them in browser with:

```bash
open -a "Google Chrome" _build/html/index.html
```

**[July, 2018]** We are actively improving our documentation. Everyone in the AZ community is 
welcome to submit a pull request to edit/fix the documentation.


##KAFKA FLOW TRIGGER
创建文件夹
```bash
/opt/azkaban/azkaban-web-server-3.91.0/plugins/dependency/kafka
```
创建文件
```bash
dependency.properties
```
文件内容
```bash
dependency.classpath=/opt/azkaban/azkaban-web-server-3.91.0/plugins/dependency/kafka/kafka-event-trigger-3.91.0-266-g28aa4940-fat.jar
dependency.class=trigger.kafka.KafkaDependencyCheck
kafka.broker.url=
```
放入jar包
```bash
kafka-event-trigger-3.91.0-266-g28aa4940-fat.jar
```
azkaban.properties中增加
```bash
proxy.user.lock.down=true
azkaban.dependency.plugin.dir=/opt/azkaban/azkaban-web-server-3.91.0/plugins/dependency
azkaban.server.schedule.enable_quartz=true
azkaban.storage.artifact.max.retention=3
org.quartz.dataSource.quartzDS.driver=com.mysql.jdbc.Driver
org.quartz.dataSource.quartzDS.URL=jdbc:mysql://10.xx.xx.xx:3306/azkaban
org.quartz.dataSource.quartzDS.user=azkaban
org.quartz.dataSource.quartzDS.password=azkaban
org.quartz.threadPool.threadCount=3
org.quartz.jobStore.class=org.quartz.impl.jdbcjobstore.JobStoreTX
org.quartz.jobStore.driverDelegateClass=org.quartz.impl.jdbcjobstore.StdJDBCDelegate
org.quartz.jobStore.tablePrefix=QRTZ_
org.quartz.jobStore.dataSource=quartzDS
```
创建conf/azkaban.private.properties,增加内容
```bash
mysql.user=azkaban
mysql.password=xx
org.quartz.dataSource.quartzDS.user=azkaban
org.quartz.dataSource.quartzDS.password=xx
```

