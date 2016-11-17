#!/usr/bin/groovy
@Library('github.com/fabric8io/fabric8-pipeline-library@master')
@Library('github.com/StayFriends/stayfriends-pipeline-library@master')

run = mavenNode() {

    sfCheckout {}
    sfMavenDeploy {}

}
