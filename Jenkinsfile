pipeline{
    agent any
   tools{
       maven 'maven'
   }
    stages{
        stage("Stage 001"){
            steps{
                echo "hey This is my first demo of pipeline"
            }
        }
        stage("Git Build"){
            steps{
                echo "code pulled from git"
            }
        }
        stage("Maven Build"){
        steps{
            sh 'mvn --version'
            sh 'mvn clean package'
            sh "mv target/*war target/myweb.war"
        }
        }

        stage("Deploy in Tomcat server"){
            steps{
               sshagent(['tomcat-new']) {
             sh """
              scp -o StrictHostKeyChecking=no target/myweb.war ubuntu@43.204.102.242:/opt/tomcat/webapps/
              ssh ubuntu@43.204.102.242  /opt/tomcat/bin/shutdown.sh
              ssh ubuntu@43.204.102.242  /opt/tomcat/bin/startup.sh
             
             """
        }
        }
    
        }
    }
}

