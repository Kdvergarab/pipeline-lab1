pipeline {
  agent any
  stages {
    
   stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: "*/$env.BRANCH"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: "$env.CREDENTIAL", url: "$env.URL_GIT"]]])
            }
        }
    stage ("Defining technology") {
      steps { echo " Selected technology is $env.TECHNOLOGY"}
        
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
}


