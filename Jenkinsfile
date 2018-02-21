pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: '35.166.210.154', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '34.209.233.6', description: 'Production Server')
         string(name: 'MODEL_PATH', defaultValue: 'Perilthing', description: 'Path to the model')
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
            when { 
                expression {
                    TO_EXECUTE = sh(
                        returnStdout: true, 
                        script: 
                        'regex="([^/]+)"; if [[ $MODEL_PATH =~ $regex ]]; then echo "RUN"; else echo "SKIP"; fi;'
                        ).trim()
                    return TO_EXECUTE == 'RUN'
                }
            }
            steps{
                sh 'echo "Now Deploying"'
            }
        }
    }
}
