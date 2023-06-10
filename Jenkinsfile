pipeline {
    agent any

    parameters {
        choice(name: 'API_NAME', choices: ['cricket-node-api', 'kabaddi-node-api', 'skillpolls-api', 'partner-wallet-api', 'node-cron-api', 'networkmodel-api', 'pred-network-node-api', 'pred-node-api', 'pred-node-corn', 'reward-cron'], description: 'Select the API')
    }

    stages {
        stage('Git ') {
            steps {
                   sh 'ssh ubuntu@172.31.51.197 "bash -x ~/scripts/gitDeployement.sh $API_NAME"'
                   sh 'pwd'
