pipeline {
    agent any

    environment {
        GOOGLE_APPLICATION_CREDENTIALS = 'G:\\Flutter Projects\\jenkins_distribution\\jenkins-distribution-credential.json'
    } 

    stages {
        stage('git pull') {
            steps {
                // Cloning the repository from GitHub
                git url: 'https://github.com/CodeCrypt05/Jenkins-Distribution',
                branch: 'main'
            }
        }

        // stage('Run Tests') {
        //     steps {
        //         // Running Flutter tests
        //         bat 'flutter test'
        //     }
        // }

        stage('Build Android APK') {
            steps {
                // Building the APK in release mode
                bat 'flutter build apk'
            }
        }
        
        stage('Archive APK') {
            steps {
                // Archiving the release APK
                archiveArtifacts artifacts: '**/build/app/outputs/flutter-apk/app-release.apk', allowEmptyArchive: false
            }
        }
        
        stage ('Distribute') {
            steps {
                // Running the Gradle commands with the environment variable set
                bat 'cd android && gradlew.bat assembleRelease appDistributionUploadRelease'
            }
        }
    }
       
    post {
        always {
            echo 'Pipeline finished.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}