pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn package'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
        stage('Build') {
            steps {
                
                sh '''
                    echo "Pushing to artifactory"
               
                '''
            }
        }
    }
}
