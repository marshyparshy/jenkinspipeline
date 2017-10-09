pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archive "**/*.war"
                }
            }
        }
        stage ('Deploy to Staging'){
            timeout(time:5, unit:'DAYS') {
                input message:'Approve deployment?', submitter: 'it-ops'
            }
            steps {
                echo 'Code deployed.'
                build job: 'Deploy-to-staging' 
            }
        }

    }
}