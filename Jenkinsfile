#Jenkins Pipeline

pipeline {
    agent { label 'atl20do0000as12.amer.prgx.com' }

    parameters {
        choice(name: 'platform', choices: ['OpenShift', 'Kubernetes'], description: 'Select the platform')
        choice(name: 'PROJECT_NAME', choices: ['mtx-dev', 'mtx-uat', 'mtx-fra', 'mtx-prod', 'wbh-dev', 'wbh-uat', 'wbh-fra', 'wbh-prod'], description: 'Select project name')
        string(name: 'CONTAINER_NAME', defaultValue: 'container1', description: 'Enter container name')
    }

    stages {
        stage('Fetch Logs') {
            steps {
                cleanWs()
                 withCredentials([usernamePassword(credentialsId: 'svcjenkins-system-github-token', usernameVariable: 'USER', passwordVariable: 'TOKEN')]) {
                    sh '''
                    git init
                    git clone https://'''+TOKEN+'''@github.com/prgxlabs/openshift-logs.git --branch TECHOPS-375 --single-branch
                    '''
                  }
                dir("openshift-logs")
                {
                sh 'pwd'  // Debug step to list files in the openshift-logs directory
                sh 'ls -l'
                sh 'chmod +x oclogs.sh'
                sh 'chmod +x kubelogs.sh'
                script {
                    if (params.platform == 'OpenShift') {
                sh "./oclogs.sh ${params.PROJECT_NAME} ${params.CONTAINER_NAME}"
                    } else if (params.platform == 'Kubernetes') {
                        sh "./kubelogs.sh ${params.PROJECT_NAME} ${params.CONTAINER_NAME}"
                    } else {
                        error('Invalid platform selection')
                    }
                  }
                }
            }
        }
    }
}

