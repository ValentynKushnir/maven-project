pipeline {
  agent any
  triggers {
    pollSCM('*/5 * * * *')
  }
  stages{
       stage ('Build'){
        steps {
          sh 'java -version'
          sh '/Users/valentynkushnir/~~tools/apache-maven-3.8.4/bin/mvn clean package'
        }
         post {
           success {
             echo 'Archiving...'
             archiveArtifacts artifacts:'**/target/*.war'
           }
         }
       }
       stage ('Deployments') {
         parallel{
           stage ('Deploy to Staging'){
             steps {
               sh "cp **/target/*.war /Users/valentynkushnir/~~tools/tomcat-stage/webapps"
             }
           }
           stage ('Deploy to prod') {
             steps {
               sh "cp **/target/*.war /Users/valentynkushnir/~~tools/tomcat-prod/webapps"
             }     
           }
         }
       }
    }
} 
  
