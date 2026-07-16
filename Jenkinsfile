pipeline {
    agent any

   stages{

    stage('Show env'){
        
        steps{

            sh 'echo $BRANCH_NAME'
            sh 'echo env.BRANCH_NAME'
            sh 'echo env.BRANCH_IS_PRIMARY'
        }
    }

   }
}
