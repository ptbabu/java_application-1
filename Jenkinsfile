pipeline {
   agent { 
               label 'slave1'
   }
   parameters {
        choice(choices: ['dev','stage','prod','master'], description: 'What environment?', name: 'select env')
    }
   
   stages {
        stage('Build') {
           
            steps {
                echo 'Building..'
                 sh 'mvn package'
                 script {
              timeout(time: 3, unit: 'MINUTES') {
                input(id: "Deploy Gate", message: "Deploy ${params.project_name}?", ok: 'Deploy')
              }
            }
        }
        }
   
        stage('Deploy') {
           
            steps {
                
                sh 'sudo apt update -y'
                sh 'sudo apt install tomcat8 -y'
                sh 'sudo apt install tomcat8-admin -y'
                sh 'sudo apt install tomcat8-user -y'
                sh 'sudo cp -f /home/ubuntu/var/lib/jenkins/workspace/pipe3/target/grants.war /var/local/tomcat8/webapps/'
                sh 'sudo cp -f /home/ubuntu/var/lib/jenkins/workspace/pipe3/tomcat-users.xml /etc/tomcat8/'
                sh 'sudo service tomcat8 restart'
            }
        }
    }
}
