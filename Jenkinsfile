pipeline{
   agent {
    docker {
      image 'maven:3.6.3-jdk-11'
      args '-v /root/.m2:/root/.m2'
    }
  }
  stages {
      stage("Maven Build"){
          steps{
              sh 'mvn -B -DskipTests clean package'
          }
      }
     
     stage('Deploy to artifactory'){
        steps{
        rtUpload(
         serverId : 'JFrog-server',
         spec :'''{
           "files" :[
           {
           "pattern":"target/*.jar",
           "target":"love"
           }
           ]
         }''',
         
      )
      }
     }
  }
        post {  
         always {  
             echo 'This will always run'  
         }  
         success {   
            echo "========Deploying executed successfully========"
            emailext attachLog: true, body: "<b>Example</b><br>Project: ${env.JOB_NAME}", from: 'nellaibala05@gmail.com', mimeType: 'text/html', replyTo: '', subject: "Deploy Success CI: Project name -> ${env.JOB_NAME}", to: "nellaibala05@gmail.com";
         }  
         failure {  
             mail bcc: '', body: "<b>Example</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: 'nellaibala05@gmail.com', mimeType: 'text/html', replyTo: '', subject: "ERROR CI: Project name -> ${env.JOB_NAME}", to: "nellaibala05@gmail.com";  
         }  
         unstable {  
             echo 'This will run only if the run was marked as unstable'  
         }  
         changed {  
             echo 'This will run only if the state of the Pipeline has changed'  
             echo 'For example, if the Pipeline was previously failing but is now successful'  
         }  
     }
     
  
        
     
    
  }

           
