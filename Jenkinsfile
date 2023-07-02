pipeline {
    agent any
   
 
    stages {

        stage("clone repo") {
            steps {
                script {
                    // Let's clone the source
                    git 'https://github.com/marwamnasri90/Marwadevops-spring-aop.git';
                }
            }
        }

        stage("mvn build") {
            steps {
                script {
                    
                    sh "mvn package -DskipTests=true"
                }
            }
        }

        stage("mvn clean") {
            steps {
                script {
                    
                    sh "mvn clean"
                }
            }
        }

        stage("Test stage") {
            steps {
                script {
                   
                   sh "mvn test"
                }
            }
        }

  	    stage("Sonar metrics") {
            steps {
                script {
                    // this step enable to execute the SonarQube analysis via a regular Maven goal
                   sh "mvn sonar:sonar "
                     }
                }
            } 
           
       stage("Deployment stage") {
            steps {
                script {
                    // this stage deploys the artifact into Nexus repository
                   sh 'mvn clean package deploy:deploy-file -DgroupId=tn.esprit -DartifactId=ExamThourayaS2 -Dversion=1.0 -DgeneratePom=true -Dpackaging=jar  -DrepositoryId=deploymentRepo -Durl=http://172.20.10.7:8081/repository/maven-releases/ -Dfile=target/ExamThourayaS2-0.0.1-SNAPSHOT.jar';              }
            }
        }
        stage('Building our image') {
            steps{
                 script {
                  sh  dockerImage = docker.build registry + ":$BUILD_NUMBER"
                 }
            }
       }
    }   
}
