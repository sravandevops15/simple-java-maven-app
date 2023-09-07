pipeline{
    agent any
    stages{
        stage("build name"){
          steps{
            script {
                    currentBuild.displayName = "${BUILD_NUMBER}-${JOB_NAME}-${BRANCH_NAME}"
                    //currentBuild.description = "continue other stages if stage fails"
                }
          }}
        stage("stage1"){
            steps{
                script {
                try {
                    sh "ech stage1"
                } catch (Exception e) {
                    continueotherstages = true
                }
               if(continueotherstages){
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                      sh "exit 1"
                }
            }
            }
            }
        }
        stage("stage2"){
            when {
                expression{
                !continueotherstages //false
                }
            }
            steps{
                sh "echo stage2"
            }
        }
        stage("stage3"){
            when {
                expression{
                continueotherstages //true
                }
				
            }
            steps{
                echo "stage3"
            }
        }
    }
}
