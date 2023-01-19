pipeline {
  agent any
    stages {
    
         stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: "*/${env.BRANCH}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github-credentials', url: "https://github.com/${env.REPOSITORY_KEY}/${env.REPOSITORY_NAME}.git"]]])
                 }
            }
      
         stage('Install Technology') {
            steps {
                script {
                                             
                        if (${env.TECHNOLOGY} == 'java') {
                       
                        agent {
                docker { image 'maven:3.8.7-eclipse-temurin-11' }
                  }
                echo "install ${env.TECHNOLOGY} success"
                 sh 'mvn --version'
                         
                        } else if (${env.TECHNOLOGY} == 'python'){
                             agent {
                docker { image 'python:3.7' }
                    }
                 echo "install ${env.TECHNOLOGY} success"
                  sh 'python --version'
                                          
                  }
                }
            }      
            
        }  
         stage('Build') {
            steps {
                sh '${MAVEN_HOME}/mvn -B -DskipTests clean package'
            }
        }       
         stage('Test') {
            steps {
                sh '${MAVEN_HOME}/mvn test'
            }
            post {
                always {
                    junit "target/surefire-reports/*.xml"
                }
            }
        }     
    }
        environment {
       
        MAVEN_HOME="/usr/share/maven/bin"
          }
}

