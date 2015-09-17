hello-samza
===========

Hello Samza is a starter project for [Apache Samza](http://samza.apache.org/) jobs.

Please see [Hello Samza](http://samza.apache.org/startup/hello-samza/0.9/) to get started.

### Setup
```
export ARTIFACTORY_URL='http://<host>:<port>/artifactory/'
export ARTIFACTORY_REPOSITORY='libs-snapshot'
export ARTIFACTORY_USER='gradle'
export ARTIFACTORY_PASSWORD='<some_pass>'
```

### Packaging/Deploying/Running 
1. ./bin/grid bootstrap
2. ./bin/grid start all
3. ./gradlew clean distTar
4. mkdir deploy/samza
5. tar -xvf build/distributions/hello-samza-0.9.1.4-SNAPSHOT-dist.tar.gz -C deploy/samza
6. deploy/samza/bin/run-job.sh --config-factory=org.apache.samza.config.factories.PropertiesConfigFactory --config-path=file://$PWD/deploy/samza/config/pubnub-app-master.properties
7. curl -H "Content-Type: application/json"  -X POST -d "{ \"job.application_id\": 1, \"job.name\" : \"foo.bar\", \"max_memory_mb\" : 512, \"max_cpu_cores\" : 1, \"needed_containers\" : 2 }" http://localhost:7778/

### Iterating with samza
from samza build/publish the subproject 
1. ./gradlew clean samza-yarn:generatePomFileForMavenJavaPublication samza-yarn:artifactoryPublish samza-core:generatePomFileForMavenJavaPublication samza-core:artifactoryPublish
from hello samza
2. rm -rf ~/.gradle/caches
3. ./gradlew clean distTar
4. rm -rf deploy/samza && mkdir deploy/samza
5. tar -xvf build/distributions/hello-samza-0.9.1.4-SNAPSHOT-dist.tar.gz -C deploy/samza
6. deploy/samza/bin/run-job.sh --config-factory=org.apache.samza.config.factories.PropertiesConfigFactory --config-path=file://$PWD/deploy/samza/config/pubnub-app-master.properties
7. curl -H "Content-Type: application/json"  -X POST -d "{ \"job.application_id\": 1, \"job.name\" : \"foo.bar\", \"max_memory_mb\" : 512, \"max_cpu_cores\" : 1, \"needed_containers\" : 2 }" http://localhost:7778/

There maybe a better way to clear gradle caches but haven't found it yet

### Pull requests and questions

[Hello Samza](http://samza.apache.org/startup/hello-samza/0.9/) is developed as part of the [Apache Samza](http://samza.apache.org) project. Please direct questions, improvements and bug fixes there. Questions about [Hello Samza](http://samza.apache.org/startup/hello-samza/0.9/) are welcome on the [dev list](http://samza.apache.org/community/mailing-lists.html) and the [Samza JIRA](https://issues.apache.org/jira/browse/SAMZA) has a hello-samza component for filing tickets.

### Contribution

To start contributing on [Hello Samza](http://samza.apache.org/startup/hello-samza/0.9/) first read [Rules](http://samza.apache.org/contribute/rules.html) and [Contributor Corner](https://cwiki.apache.org/confluence/display/SAMZA/Contributor%27s+Corner). Notice that [Hello Samza](http://samza.apache.org/startup/hello-samza/0.9/) git repository does not support git pull request.
