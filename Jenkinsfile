pipeline {
  agent any
  stages {
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
                echo "$env.JAVA"
                         
                        } else if (env.TECHNOLOGY == 'python'){
                             agent {
                docker { image 'python:3.7' }
            }
            echo "$env.PYTHON"
            sh 'python --version'
                                          
                }
            
            }
    }}
}
}