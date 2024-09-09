
pipeline {
    agent{label 'jenkins-Agent'}
    tools {
      jdk 'java17'
      maven 'Maven3'
    }
    stages{
      stage("cleanup Workspace"){
          step {
          cleanWs()
           } 
     }
     
    stages("checkout form SCM"){
         steps{
         git branch: 'main', credentialsId; 'github', url: 'https://github.com/Lokendrasaini/jenkins-cicd.git'
          }
    }
     
     stages("Test Application"){
          steps {
            sh "mvn clean package" 
           }
    }
    
      stages("Test Application"){
          steps {
            sh "mvn test" 
           }
    }
    
    
  }


}
  
