def Build (technology){
    switch(technology) {
        case "Maven":
            sh '''
                mvn --v
                mvn -B -DskipTests clean package
                cd $WORKSPACE/target/
                mv my-app-1.0-SNAPSHOT.jar deployment-java-$BUILD_NUMBER.jar
                ls -lt
            '''            
        break
        case 'Python':
            sh '''
                pwd 
                python --version
                pwd
                python -m pip install --upgrade pip
                pip install -r requirements.txt
                python -m compileall
                
            '''
        break
        default:
            sh 'Not Found'
        break
    }
}

def Tests(technology){
    switch(technology) {
        case 'Maven':
            sh 'mvn test'
            
        break
        case 'Python':
            sh'nosetests -v int_test'
    }
}

def SonarQube(technology){
    switch(technology) {
        case 'Maven':
              sh '''
                     mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar \
                    -Dsonar.projectKey=$TECHNOLOGY \
                    -Dsonar.projectName=$TECHNOLOGY \
                    -Dsonar.projectVersion=1.0 \
                    -Dsonar.sourceEncoding=UTF-8
                    '''
            
        break
        case 'Python':
            sh '''
            sonar-scanner \
            -Dsonar.lenguage=py \
            -Dsonar.projectKey=$TECHNOLOGY\
            -Dsonar.projectName=$TECHNOLOGY\
            -Dsonar.sourceEnconding=UTF-8 \
            -Dsonar.projectVersion=0.1 \
            '''
            
        break
    }
}






pipeline {

  agent any 
  

  stages {
    stage('Image Config') {
      steps {
        script {
          if (env.TECHNOLOGY == 'Maven') {
            dockerImage = "maven:3.8.7-eclipse-temurin-11-alpine"
            println "install $env.TECHNOLOGY success"
          } else if (env.TECHNOLOGY == 'Python') {
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
                      
                     checkout([$class: 'GitSCM', branches: [[name: "*/$env.BRANCH"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github-credentials', url: "https://github.com/${env.REPOSITORY_KEY}/${env.REPOSITORY_NAME}.git"]]])
                     
                    }
                }
               stage('Build'){
                   steps {
                        print " Build $env.TECHNOLOGY"
                        Build ("${TECHNOLOGY}")
                   }
                 }
                   
                stage('Tests'){
                    steps {
                            print "Test $env.TECHNOLOGY"
                            Tests ("${TECHNOLOGY}")                               
                                }

                    post {
                          always {
                                     junit 'target/surefire-reports/*.xml'
                                }
                         }
                }  

                stage('SonarQube'){
                      steps{  
                    withSonarQubeEnv(installationName: 'sonarqube'){
                        SonarQube("${TECHNOLOGY}")
                    }
                    
                                            
                                                }
               }
             }
            }
        }
        
    }
