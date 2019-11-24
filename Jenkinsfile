pipeline {
   agent any
   parameters {
        choice(choices: ['dev','stage','prod'], description: 'What environment?', name: 'select env')
    }
   
   stages {
        stage('Build') {
           
            steps {
                echo 'Building..'
                 sh 'mvn package'
                 script {
              timeout(time: 1, unit: 'MINUTES') {
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
                sh 'sudo cp /home/ubuntu/workspace/Deployment/target/grants.war /var/lib/tomcat8/webapps/'
                sh 'sudo cp /home/ubuntu/workspace/Deployment/tomcat-users.xml /etc/tomcat8/'
                sh 'sudo service tomcat8 restart'
            }
        }
    }
}
