// CODE_CHANGES = getGitChanges();
pipeline {
    agent any
    environment {
        NEW_VERSION = '1.0.0'
        SEVER_CRENDENTIALS = credentials('ravuthz-password')
    }
    parameters {
        string(name: 'GREETING', defaultValue: 'Hello', description: 'How should I greet the world?')
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanParam(name: 'EXECUTE_TESTS', defaultValue: true, description: '')
    }
    stages {
        stage("clone") {
            steps {
                echo "crendetials => ${SEVER_CRENDENTIALS} ${SEVER_CRENDENTIALS_USR} ${SEVER_CRENDENTIALS_PSW}"
                git "https://ravuthz@bitbucket.org/local-projects/micro-fin-admin.git"
            }
        }
        stage("build") {
            // when {
            //     expression {
            //         BRANCH_NAME == 'develop' && CODE_CHANGES == 'master'
            //     }
            // }
            steps {
                echo "building the application ..."
                echo "build version ${NEW_VERSION}"
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            }
        }
        stage("test") {
            when {
                expression {
                    params.EXECUTE_TESTS == true
                }
            }
            steps {
                echo "when branch name equals to 'develop'"
                echo "testing the application ..."
            }
        }
        stage("deploy") {
            steps {
                echo "now deploy the application ..."
                echo "now deploying version ${params.VERSION}"
                // withCredentials([
                //     usernamePassword(credentials: 'ravuthz-password', usernameVariable: USR, passwordVariable: PWD) 
                // ]) {
                //     sh "Echo script ${USR} ${PWD}"
                // }
            }
        }
    }
    post {
        always {
            echo "post always"
        }
        unstable {
            echo "post unstable"
        }
        failure {
            echo "post failure"
        }
        success {
            echo "post success"
        }
        changed {
            echo "post changed"
        }
    }
}