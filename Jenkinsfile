pipeline{
    agent any
    stages {
        // stage("Code analysis & Unit Test") {

        //     failFast true

        //     parallel {
        //         stage("Currency") {
        //             agent {
        //                 label "jenkins-agent-python-3"
        //             }
        //             steps {
        //                 dir("currency") {
        //                     sh "pip3 install -r requirements.txt"
        //                     sh "./scripts/lint"
        //                     sh "./scripts/test"
        //                 }
        //             }
        //         }

        //         stage('History') {
        //             agent {
        //                 label "jenkins-agent-node-14"
        //             }
        //             steps {
        //                 dir("history") {
        //                     sh "npm ci"
        //                     sh "npm run lint"
        //                     sh "npm test"
        //                 }
        //             }
        //         }

        //         stage('Exchange') {
        //             steps {
        //                 dir("exchange") {
        //                     sh "./mvnw clean verify"
        //                 }
        //             }
        //         }
        //     }
        // }

        // stage("Deploy to Stage") {

        //     failFast true

        //     parallel {
        //         stage("Currency") {
        //             steps {
        //                 sh """
        //                     oc start-build currency --follow --wait -n rht-jramirez-exchange-stage
        //                 """
        //             }
        //         }

        //         stage("History") {
        //             steps {
        //                 sh """
        //                     oc start-build history --follow --wait -n rht-jramirez-exchange-stage
        //                 """
        //             }
        //         }

        //         stage("News") {
        //             steps {
        //                 sh """
        //                     oc start-build news --follow --wait -n rht-jramirez-exchange-stage
        //                 """
        //             }
        //         }

        //         stage("Exchange") {
        //             steps {
        //                 dir("exchange") {
        //                     sh """
        //                         oc project rht-jramirez-exchange-stage
        //                         ./mvnw clean package -DskipTests -Dquarkus.kubernetes.deploy=true -Dquarkus.openshift.expose=true
        //                     """
        //                 }
        //             }
        //         }

        //         stage("Frontend") {
        //             steps {
        //                 sh """
        //                     oc start-build frontend --follow --wait -n rht-jramirez-exchange-stage
        //                 """
        //             }
        //         }

        //     }
        // }


        stage("Functional Tests") {
            agent {
                label "jenkins-agent-cypress"
            }

            environment {
                BASEURL = "http://exchange-rht-jramirez-exchange-stage.apps.na45-stage.dev.nextcle.com/"
            }

            steps {
                dir("frontend") {
                    sh "npm ci"
                    sh "npm run test:functional"
                }
            }
        }
    }
}