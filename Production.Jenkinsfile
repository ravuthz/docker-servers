pipeline {
    agent any
    environment {
        SPRING_PROFILE = "prd"
        TOMCAT_CRENDENTIALS = credentials('tomcat-adminz')
        TOMCAT_FILE = "./i-collector/target/i-collector-2.0-SNAPSHOT.war"
        TOMCAT_PATH = "/i-collector"
        TOMCAT_URI = "192.168.99.84:8080"
    }
    stages {
        stage('Clone Project') {
            steps {
                echo 'Clone Project'
                checkout([$class: 'GitSCM', branches: [[name: '*/develop']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'ravuthz-bitbucket', url: 'git@bitbucket.org:local-projects/i-finance.git']]]) 
            }
        }
        stage('Clean & Build Project') {
            steps {
                sh """
                    echo "SPRING_PROFILE: ${env.SPRING_PROFILE}"
                    
                    rm -rf ./i-collector/node_modules
                    npm install --prefix ./i-collector
    
                    mvn -pl core,i-collector clean package -Pproduction -T1C -Dmaven.test.skip=true
                """
            }
        }
        stage('Deploy Project to Tomcat') {
            steps {
                sh """
                curl -s --upload-file $TOMCAT_FILE "http://${TOMCAT_CRENDENTIALS}@${TOMCAT_URI}/manager/text/deploy?path=${TOMCAT_PATH}&update=true"
                """
                // sshagent(credentials('tomcat-adminz')) {
                //     sh 'ssh -o StrictHostKeyChecking=no -l root@192.168.99.65 uname -a'
                //     sh 'scp -o StrictHostKeyChecking=no target/*.war root@192.168.99.65:~/dockers/tomcat/webapps/i-collector.war'
                // }
            }
        }
    }
}
