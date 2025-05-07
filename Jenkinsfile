pipeline {
    agent any

    tools {
        maven 'Maven'  // Ensure this matches Jenkins' Maven installation name
    }

    environment {
        // Add DISPLAY variable in case it's needed by xvfb-run or GUI processes
        DISPLAY = ':99'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Thushardm/SauceDemoAutoMaven.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                // Use xvfb-run to emulate a display for Chrome in headless environments
                sh 'xvfb-run -a mvn test'
            }
        }

        stage('Run Application') {
            steps {
                // Run your main class (should be safe now with Chrome headless setup)
                sh 'mvn exec:java -Dexec.mainClass=com.example.App'
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
