pipeline{
    agent any

    tools {
        maven 'Maven 3.3.9'
    }

    stages{
        stage("Build"){
            steps{
                sh 'mvn clean install -DskipTests'
            }
            post{
                success{
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('UNIT TEST'){
            steps {
                sh 'mvn test'
            }
        }

        stage('INTEGRATION TEST'){
            steps {
                sh 'mvn verify -DskipUnitTests'
            }
        }

        stage ('CODE ANALYSIS WITH CHECKSTYLE'){
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
            post {
                success {
                    echo 'Generated Analysis Result'
                }
            }
        }
        
    }
    post{
        always{
            echo "========my pieline========"
        }
    }
}
