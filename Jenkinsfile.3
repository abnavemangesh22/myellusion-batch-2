pipeline{
    agent any 
    tools{
        maven 'M3'
    }
    environment{
        scannerHome = tool 'SonarScanner'
    }
    stages{
        stage('Code Pull'){
            steps{
                //cleanWs()
                //sh 'git clone https://github.com/abnavemangesh22/MyNewPetClinic-2.git'
                git changelog: false, poll: false, url: 'https://github.com/abnavemangesh22/MyNewPetClinic-2.git'
            }
        }
        stage('Code Compile'){
            steps{
                sh 'mvn clean test'
            }
        }
        stage('Composition Analysis'){
            steps{
                dependencyCheck additionalArguments: '--format HTML', odcInstallation: 'dependency'
            }
        }
        stage('Static Code Analysis'){
            steps{
              script{
                 withSonarQubeEnv(credentialsId: 'sonar') {
                    sh 'echo $SONAR_HOST_URL'
                    sh 'echo $SONAR_AUTH_TOKEN'
                    sh '${scannerHome}/bin/sonar-scanner -D sonar.projectKey=EllusionProject -Dsonar.java.binaries=target/classes'
                 }
              }
            }
        }
        stage('Code Package'){
            steps{
                sh 'mvn package -Dmaven.test.skip'
            }
        }
        stage('Nexus Uploader'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'spring-petclinic', classifier: '', file: 'target/spring-petclinic-1.5.2.jar', type: 'jar']], credentialsId: 'nexusserver', groupId: 'org.springframework.samples', nexusUrl: '15.206.157.27:32768', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-releases', version: '1.5.2'
            }
        }
        stage('Docker Build Activity'){
            steps{
                sh 'docker info'
                sh 'docker ps -a'
                sh 'docker build -t mangeshabnave/myellusionimage-$BUILD_NUMBER .'
            }
        }
        stage('Upload Image to Hub'){
            steps{
              withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'password', usernameVariable: 'username')]) {
                    sh "docker login -u ${env.username} -p ${env.password}"
                    sh "docker push mangeshabnave/myellusionimage-$BUILD_NUMBER"
                }  
            }
        }
        stage('Run on the Test Env'){
            steps{
                sh 'docker -H tcp://172.31.38.84:2375 pull mangeshabnave/myellusionimage-$BUILD_NUMBER'
                sh 'docker -H tcp://172.31.38.84:2375 run -dit -P mangeshabnave/myellusionimage-$BUILD_NUMBER'
            }
        }
        
    }
}
