pipeline {
    agent any

    tools { nodejs "NodeJS16"}
    environment {
        NODE_ENV = "production"   
    }
    stages {
        stage('source') {
            steps {
                git branch: 'main', url: 'https://github.com/mcoria08/testproject'
                echo "Show content of test.txt file"
                sh 'cat test.txt'
            }
        }
        
        stage('build') {
            environment{
                NODE_ENV = 'staging'
            }
            steps {
                echo NODE_ENV
                 withCredentials([string(credentialsId: 'e66ca7bf-ae9f-4005-b74b-323db5890adc', variable: 'secureVerificationWithTextCredential')]) {
                    // some block
                    echo secureVerificationWithTextCredential
                }
                sh 'npm install'
            }
        }
        
        stage('saveArtifact') {
            steps {
                archiveArtifacts artifacts: '**', followSymlinks: false
            }
        }
    }
}
