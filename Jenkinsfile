#!/usr/bin/env groovy

properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '60', numToKeepStr: '10')), disableConcurrentBuilds() ])

node('xcode14') {
    ansiColor('xterm') {
        timestamps {
            timeout(5) {
                stage('Clean Workspace') {
                    cleanWs()
                }

                stage('Checkout Project') {
                    checkout scm
                }

                if(env.BRANCH_NAME in ['cerner-release', 'release-candidate']) {
                    stage('Push To Cocoapod Spec Repo') {
                        sh library('ios-jenkins-build').com.cerner.ios.Cocoapods.manualPodPushCommand()
                    }
                }
                else {
                    stage('No Pushing from this branch') {
                        //No-Op
                    }
                }
            }
        }
    }
}
