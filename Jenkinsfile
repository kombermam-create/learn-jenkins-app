pipeline {
    agent any

    options {
        preserveStashes(buildCount: 5)
    }

    stages {
        stage('Testing') {
            steps {
                script {
                    docker.image('nginx:latest') { nginx ->

                        sh 'echo "Running tests, nginx starting..."'
                        sh 'pwd'
                    }

                    docker.image('curlimages/curl').inside { "--link ${nginx.id}:nginx" ->
                        sh '''
                            for i in {1..10}; do
                                echo "Attempt $i: Testing nginx response..."
                                curl -s http://nginx | grep -q "Welcome to nginx!" && echo "Nginx is up and running!" || echo "Nginx is not responding."
                                sleep 2
                            done
                        '''


                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            cleanWs()
        }
    }
}