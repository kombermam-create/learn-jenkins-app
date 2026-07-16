pipeline {
    agent any

    stages {
        stage('Buiild npm') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            environment {
                npm_config_cache = "${WORKSPACE}/.npm-cache"
            }
            steps {
                sh '''
                    pwd
                    ls -la
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage("Tests")
        {
            parallel{
                
                stage("Test app and file"){
                    agent{
                        docker{
                            image 'node:18-alpine'
                            reuseNode true
                        }
                    }
                    environment {
                        npm_config_cache = "${WORKSPACE}/.npm-cache"
                    }
                    steps{
                        sh 'test -f public/index.html' 
                        sh 'npm --version'
                        sh 'npm test'
                    }

                }
                stage("Bogdans stage")
                {
                    
                    steps{
                        sh "echo hello world"
                    }

                }
                


            }
        }

    }
    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}
