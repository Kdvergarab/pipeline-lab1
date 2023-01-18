pipeline {
  agent any
  stages {
    
   stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: "*/$env.branch"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: "$env.credential", url: "https://github.com/Kdvergarab/pipeline-lab1.git"]]])
            }
        }
    stage ("Defining technology") {
      steps {
        script {
          env.TECHNOLOGY = input message: 'Please enter the Technology to use',
                             parameters: [string(defaultValue: '',
                                          description: '',
                                          name: 'Technology')]
              }
        }
    }
    stage('Install Technology') {
            steps {
                script {
                                             
                        if (env.TECHNOLOGY == 'java') {
                       
                        agent {
                docker { image 'maven:3.8.7-eclipse-temurin-11' }
            }
                echo "install $env.TECHNOLOGY success"
                 sh 'mvn --version'
                         
                        } else if (env.TECHNOLOGY == 'python'){
                             agent {
                docker { image 'python:3.7' }
            }
            echo "install $env.TECHNOLOGY success"
             sh 'python --version'
                                          
                }
            
            }
     
              
              
            
        }         
              
    }}
}

