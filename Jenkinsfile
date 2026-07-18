pipeline {
    agent any

    options {
        preserveStashes(buildCount: 5)
    }

    stages {
        stage('Pull latest and push branch tag') {
            steps {
                script {
                    // BRANCH_NAME доступна переважно в Multibranch Pipeline
                    def branchName = env.BRANCH_NAME
                    sh '''
                        echo "Current directory:"
                        pwd

                        echo "Files:"
                        ls -la
                    '''

                    // Docker tag не може містити "/", наприклад feature/login.
                    // feature/login -> feature-login
                    def safeBranchName = branchName
                        .toLowerCase()
                        .replaceAll('[^a-z0-9_.-]', '-')

                    def repository = 'bogd123bogdan/bkuzmyshen_application'
                    def sourceImageName = "${repository}:latest"

                    docker.withRegistry(
                        'https://index.docker.io/v1/',
                        'dockerhub'
                    ) {
                        // Об'єкт image: bogd123bogdan/bkuzmyshen_application:latest
                        def image = docker.image(sourceImageName)

                        // docker pull bogd123bogdan/bkuzmyshen_application:latest
                        image.pull()

                        // docker tag ...:latest ...:<branch>
                        image.tag(safeBranchName)

                        // docker push bogd123bogdan/bkuzmyshen_application:<branch>
                        image.push(safeBranchName)
                    }
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