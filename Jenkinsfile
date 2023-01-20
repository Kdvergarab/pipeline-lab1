pipeline {

  agent any 

  stages {
    stage('Image Config') {
      steps {
        script {
          if (env.TECHNOLOGY == 'java') {
            dockerImage = "maven:3.8.7-eclipse-temurin-11"
            println "install $env.TECHNOLOGY success"
          } else if (env.TECHNOLOGY == 'python') {
            dockerImage = "python:3.7"
            println "install $env.TECHNOLOGY success"
          } else {
            println "Please select a technology"
          }
        }
      }
    }
    stage('Image Install') {
        agent {
          docker {
            image "${dockerImage}"
            args "-u 0:0" // Force container user root
            }}
            stages{
                stage('Checkout'){
                    steps{ 
                      
                     checkout([$class: 'GitSCM', branches: [[name: "*/main"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github-credentials', url: "https://github.com/Kdvergarab/pipeline-lab1.git"]]])
                     
                    }
                }
               stage('Build'){
                    steps{
                            sh "hostname" 
                            
                        } }
                stage('Tests'){
                    steps {
                                sh "hostname"
                                }
                            
                        }
                stage('SonarQube'){
                      steps{  sh "hostname"
                            }
                            }
                            }
                            }
                            }
        
    }
   
