pipeline{
    agent any
    environment{
        Version = "${env.BUILD_ID}"
    }
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
                    // withCredentials([string(credentialsId: 'nexus-password', variable: 'nexus-credentials')]) {
                    //     sh ''' 
                    //     docker build -t 172.105.43.25:8083/springapp:${Version} .
                
                    //     docker login -u admin -p $nexus-credentials 172.105.43.25:8083

                    //     docker push 172.105.43.25:8083/springapp:${Version}

                    //     docker rmi 172.105.43.25:8083/springapp:${Version}
                    //     '''
                    // }
                    sh ''' 
                        docker build -t 172.105.43.25:8083/springapp:${Version} .
                
                        docker login -u admin -p nexus 172.105.43.25:8083

                        docker push 172.105.43.25:8083/springapp:${Version}

                        docker rmi 172.105.43.25:8083/springapp:${Version}
                        '''
                }
            }
        }
    }

}
