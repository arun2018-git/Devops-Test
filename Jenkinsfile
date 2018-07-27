pipeline {
    agent any
      stages {
        stage("checkout"){
            steps {
                checkout scm
            }
        }

       stage("build docker image"){
            steps {
                sh " docker build -f Dockerfile -t codeassesment ."
            }
        }
         
        stage("static code analysis"){
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh '/opt/sonar/bin/sonar-scanner -Dsonar.projectKey=f275f9da59b48b9babf5cf4c61a3e594abbae833 -Dsonar.sources=.'
                }
            }
        }
        stage("env cleanup"){
            steps {
                sh "  docker rm -f codeassesment"
            }
        }
        stage("Launch service"){
            steps {
                sh " docker run -d --name codeassesment codeassesment"
                sh " docker logs codeassesment"
            }
        }
        stage("Launch Info"){
            steps {
                echo "http://13.126.236.71:4020"
            }
        }
    }
}

