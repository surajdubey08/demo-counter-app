pipeline{
    agent any

    stages {
        stage('Sonar quality status'){
            // agent{
            //     docker{
            //         image 'maven'
            //     }
            // }
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
        
        stage('Quality Gate status'){
            steps{
                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                }
            }
        }

        stage('Docker build & docker push to Nexus repo'){
            steps{
                script{
                    
                }
            }
        }
    }

}
