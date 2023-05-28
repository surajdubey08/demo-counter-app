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
                        // sh 'mvn clean package sonar:sonar'
                        withMaven {
                            sh "mvn clean package sonar:sonar"
                        }
                    }
                }
            }
        }
    }
}
