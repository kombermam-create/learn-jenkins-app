pipeline {
    agent any
    options {
        preserveStashes(buildCount: 5)
    }
    stages {
        stage('Build') {
            steps {
                mkdir -p build
                sh 'echo "Building..." > build/build.log' 
                stash includes: 'build/build.log', name: 'build-log'
            }
        }
        stage('Test') {
            steps {
                unstash 'build-log'
                ls -la
                sh 'cat build/build.log'
                echo 'Running tests...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                unstash 'build-log'
                ls -la
            }
        }
    }
}