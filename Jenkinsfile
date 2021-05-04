pipeline{
    agent{
        label 'deployment-tools'
    }
    environment{
        PROD_PROJECT="prod-svr"
        COMMIT_ID = sh(returnStdout: true, script: "git log -n 1 --pretty=format:'%h'").trim()
    }
    

    stages{
        stage("Prod Approval") {
            steps{
                script {                    
                    try {
                        timeout(time:30, unit:'MINUTES') {
                            env.APPROVE_PROD = input message: 'Deploy to Production', ok: 'Continue',
                                parameters: [choice(name: 'APPROVE_PROD', choices: 'YES\nNO', description: 'Deploy service to PRODUCTION?')]
                            if (env.APPROVE_PROD == 'YES'){
                                env.DPROD = true
                            } else {
                                env.DPROD = false
                                return false
                            }
                        }
                    } catch (error) {
                        env.DPROD = false
                        echo 'Timeout has been reached! Deploy to PRODUCTION automatically blocked due to lack of approval'
                        return false
                    }
                } 
            }
        }
        

        stage('Check/Create namespace and secrets') {
            steps{
                script{
                    echo 'next stage'
                }
            }
        }
    }
}
