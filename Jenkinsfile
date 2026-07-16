pipeline {
    agent any

   stages {

    stage('Show env'){
        agent {
            docker {
                image 'alpine:latest'
            }
        }
        steps{
            sh '''
            mkdir somefolder
            touch somefolder/somefile
            touch somefolder/somefile2
            touch somefolder/somefile3
            mkdir somefolder/somefolder2
            mkdir somefolder/somefolder2/somefolder3
            touch somefolder/somefolder2/somefolder3/text.txt
            '''
            stash includes: 'somefolder/*', name: 'mystash'
        }
    }
     stage('Show env2'){
        agent {
            docker {
                image 'johnfmorton/tree-cli'
            }
        }
        steps {
            unstash 'mystash'
            sh 'tree .'
        }
    }

   }
}
