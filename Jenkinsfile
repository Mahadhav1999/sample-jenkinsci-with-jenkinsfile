pipeline {
    agent any   // Run on any available Jenkins agent (or master)

    stages {
        stage('Checkout') {
            steps {
                // Pull code from GitHub
                git branch: 'main', url: 'https://github.com/Mahadhav1999/java-hello-world.git'
            }
        }

         stage('Compile') {
            steps {
                echo 'compiling the file...'
                sh javac hello.java > build_output.txt'
            }
        }

        stage('Build & Run') {
            steps {
                echo 'Building the file with output...'
                sh java Main > build_output.txt'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Example: Run a dummy test
                sh 'if grep -q "Hello Jenkins" build_output.txt; then echo "Test Passed"; else exit 1; fi'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to environment...'
                // Dummy deploy step
                sh 'echo "Deployed successfully!"'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline completed successfully!'
        }
        unstable {
            echo '⚠️ Build is unstable (tests or quality checks failed)'
        }
        failure {
            echo '❌ Pipeline failed!'
        }
    }
}
