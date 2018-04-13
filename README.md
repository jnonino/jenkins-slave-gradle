# Jenkins Slave Gradle #

Jenkins Slave for Gradle builds. Docker image based on Gradle official image.

	https://hub.docker.com/r/jnonino/jenkins-slave-gradle/

## Docker Image Tags ##

-	[`jdk-alpine` (*jdk-alpine/Dockerfile*)](https://github.com/jnonino/jenkins-slave-gradle/blob/master/jdk-alpine/Dockerfile)
-	[`jdk` (*jdk/Dockerfile*)](https://github.com/jnonino/jenkins-slave-gradle/blob/master/jdk/Dockerfile)
-	[`jdk10` (*jdk10/Dockerfile*)](https://github.com/jnonino/jenkins-slave-gradle/blob/master/jdk10/Dockerfile)
-	[`jdk9` (*jdk9/Dockerfile*)](https://github.com/jnonino/jenkins-slave-gradle/blob/master/jdk9/Dockerfile)
-	[`jdk8-alpine` (*jdk8-alpine/Dockerfile*)](https://github.com/jnonino/jenkins-slave-gradle/blob/master/jdk8-alpine/Dockerfile)
-	[`jdk8` (*jdk8/Dockerfile*)](https://github.com/jnonino/jenkins-slave-gradle/blob/master/jdk8/Dockerfile)
-	[`jdk7-alpine` (*jdk7-alpine/Dockerfile*)](https://github.com/jnonino/jenkins-slave-gradle/blob/master/jdk7-alpine/Dockerfile)
-	[`jdk7` (*jdk7/Dockerfile*)](https://github.com/jnonino/jenkins-slave-gradle/blob/master/jdk7/Dockerfile)

## Tools Installed ##

- Gradle
- Open Java JDK 8
- Git
- Mercurial
- Subversion
- wget
- curl
- unzip
- OpenSSH
- CA Certificates

## Add certificate to connect to HTTPS repositories

To add custom certificates and root CAs, create a new Dockerfile and import them with the following code.

	FROM jnonino/jenkins-slave-gradle
	LABEL maintainer="Julian Nonino <noninojulian@outlook.com>"

	# Trust Root CA
	COPY Root_CA.crt /tmp
	RUN keytool -importcert -alias Root_CA -keystore ${JAVA_HOME}/jre/lib/security/cacerts -storepass changeit -file /tmp/Root_CA.crt -noprompt && \
		cp /tmp/Root_CA.crt /usr/local/share/ca-certificates/ && \
		chmod 644 /usr/local/share/ca-certificates/Root_CA.crt && \
		update-ca-certificates

	CMD ["/bin/bash"]
