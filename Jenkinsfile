pipeline {
  agent any
  stages {
    
   stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: "*/main"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github-node1', url: "https://github.com/Kdvergarab/pipeline-lab1.git"]]])
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
                          env.PYTHON= "PAYTHON"
                          env.JAVA="JAVA" 
                    
                        if (env.TECHNOLOGY == 'java') {
                       
                        agent {
                docker { image 'maven:3.8.7-eclipse-temurin-11' }
            }
                echo "install $env.JAVA success"
                 sh 'mvn --version'
                         
                        } else if (env.TECHNOLOGY == 'python'){
                             agent {
                docker { image 'python:3.7' }
            }
            echo "install $env.PYTHON success"
             sh 'python --version'
                                          
                }
            
            }
     
              sh 'python --version'
              
            
        }         
              
    }}
}
}
