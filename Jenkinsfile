pipeline{
    agent any
    tools{
        maven 'M3'
    }
    stages{
        stage('git checkout'){
            steps{
             //cleanWs()
             //sh "git clone https://github.com/abnavemangesh22/ellusion-project-dev-1.git"   
             git changelog: false, poll: false, url: 'https://github.com/abnavemangesh22/ellusion-project-dev-1.git'
            }
        }
        stage('code compile'){
            steps{
              sh "mvn compile"
            }
        }
        stage('code analysis'){
            environment{
                scannerHome = tool 'sonar'
            }
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonartoken') {
                      sh "echo $SONAR_HOST_URL"
                      sh "echo $SONAR_AUTH_TOKEN"
                      sh "${scannerHome}/bin/sonar-scanner -D sonar.projectKey=MangeshEllusion -Dsonar.java.binaries=target/classes"
                    }
                }
            }
        }
        
        stage('build stage'){
            steps{
                sh "mvn package"
            }
        } 
        stage('build dockerfile'){
            steps{
                sh "docker build -t mangeshabnave/mytestpet-ellusion-$BUILD_NUMBER ."
                sh "docker images"
            }
        }
        stage('Upload the Image'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'password', usernameVariable: 'username')]) {
                   sh "docker login -u ${env.username} -p ${env.password}" 
                   sh "docker push mangeshabnave/mytestpet-ellusion-$BUILD_NUMBER"
                }
            }
        }
    }
}
