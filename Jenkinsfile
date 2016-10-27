#!/usr/bin/groovy


def versionPrefix = ""
try {
  versionPrefix = VERSION_PREFIX
} catch (Throwable e) {
  versionPrefix = "1.0"
}

def canaryVersion = "${versionPrefix}.${env.BUILD_NUMBER}"
def utils = new io.fabric8.Utils()

node {

  stage 'Checkout'
  checkout scm

  echo 'NOTE: running pipelines for the first time will take longer as build and base docker images are pulled onto the node'
  kubernetes.pod('buildpod').withImage('fabric8/maven-builder')
      .withPrivileged(true)
      .withHostPathMount('/var/run/docker.sock','/var/run/docker.sock')
      .withEnvVar('DOCKER_CONFIG','/home/jenkins/.docker/')
      .withSecret('jenkins-docker-cfg','/home/jenkins/.docker')
      .withSecret('jenkins-maven-settings','/root/.m2')
      .withServiceAccount('jenkins')
      .inside {

    stage 'build' 
    sh "mvn package"

    stage 'deploy' 
    sh "mvn deploy"

  }
}
