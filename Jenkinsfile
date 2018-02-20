pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: '35.166.210.154', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '34.209.233.6', description: 'Production Server')
         string(name: 'MODEL_PATH', defaultValue: 'models/stuff/Perilthing/model/submodel', description: 'Path to the model')
    }

    triggers {
         pollSCM('* * * * *')
     }

stages{
        stage('Build'){
            steps {
                sh 'echo "Now Building"'
                //sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    //archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            when { ${BUILD_LOG_REGEX,regex="Keep one snapshot per week"} }
            }
            steps{
                sh 'echo "Now Deploying"'
            }
        }
    }
}
