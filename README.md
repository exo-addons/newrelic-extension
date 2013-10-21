eXo Platform integration with NewRelic
===================

This extension aims to simplify [NewRelic](http://newrelic.com/) integration with [eXo Platform 4](http://www.exoplatform.com)

The examples in this documentation use the Tomcat version of [eXo Platform 4](http://www.exoplatform.com) and and a *nix operating system.

Build
===============

Prerequisite : install [Maven 3](http://maven.apache.org/download.html)

```
git clone https://github.com/exo-addons/newrelic-extension.git
cd newrelic-extension
mvn clean install
```

The extension binary is now available at ```<NEWRELIC_GIT_HOME>/pkg/target/newrelic-extension-pkg-XXXXXXXXXX.zip```

Install
===============

Prerequisite : install [eXo Platform 4](http://www.exoplatform.com/company/en/download-exo-platform) (tomcat version is used in this page)

Unzip the NewRelic extension built on the previous step in ```$EXO_PLATFORM_HOME/extensions/``` and ask eXo Platform installer to deploy it

```
unzip $NEWRELIC_GIT_HOME/pkg/target/newrelic-extension-pkg-XXXXXXXXXX.zip -d $EXO_PLATFORM_HOME/extensions/
cd $EXO_PLATFORM_HOME
./extension.sh -i newrelic
```

Configure
===============

Create your newrelic.yml configuration file to ```$EXO_PLATFORM_HOME/conf/``` and [configure newrelic](https://docs.newrelic.com/docs/java/java-agent-configuration) as you need ([newrelic.yml template](https://docs.newrelic.com/docs/java/java-agent-config-file-template))

Add the NewRelic agent in the eXo Platform at the end of the following file : ```$EXO_PLATFORM_HOME/bin/setenv-customize.sh``` (if this file doesn't already exists, rename ```$EXO_PLATFORM_HOME/bin/setenv-customize.sample.sh``` to ```$EXO_PLATFORM_HOME/bin/setenv-customize.sh```)

```
...

# NewRelic
CATALINA_OPTS="${CATALINA_OPTS} -javaagent:${CATALINA_HOME}/lib/newrelic-agent-3.0.1.jar"
CATALINA_OPTS="${CATALINA_OPTS} -Dnewrelic.config.file=${CATALINA_HOME}/conf/newrelic.yml"
CATALINA_OPTS="${CATALINA_OPTS} -Dnewrelic.config.log_file_path=${CATALINA_HOME}/logs"
CATALINA_OPTS="${CATALINA_OPTS} -Dnewrelic.config.log_daily=true"
CATALINA_OPTS="${CATALINA_OPTS} -Dnewrelic.config.log_file_count=5"
CATALINA_OPTS="${CATALINA_OPTS} -Dnewrelic.config.log_limit_in_kbytes=1024
```

Run
===============

Launch [eXo Platform 4](http://www.exoplatform.com) with its startup script : ```$EXO_PLATFORM_HOME/start_eXo.sh``` ( use ```$EXO_PLATFORM_HOME/start_eXo.sh -h``` for more options)

Use your eXo Platform so that NewRelic agent could collect some metrics and then go to your [NewRelic Dashboard](https://rpm.newrelic.com) to see metrics ...

**You are now ready to use NewRelic with [eXo Platform 4](http://www.exoplatform.com)**