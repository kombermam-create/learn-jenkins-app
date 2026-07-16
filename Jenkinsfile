pipeline {
    agent any

   stages{

    stage('Show env'){
        environment {
            NAME = credentials("name")
        }
        steps{

            sh 'echo $BRANCH_NAME'
            sh 'echo $BRANCH_IS_PRIMARY'
            sh "echo $NAME"
            sh 'echo $NAME > secret.txt'
            sh 'cat secret.txt'

        }
    }

   }
}
