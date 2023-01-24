
pipeline {
    agent { label "master" }

    parameters {
        choice(choices: ['start', 'rebuild', 'stop'], name: 'Status')
    }

    stages {
        stage('Run Snappass service') {
            steps {
                script {
                    if (params.Status == 'start') {
                        echo 'Build Snappass service'
                        sh "docker-compose up -d --build --remove-orphans"
                    } else if (params.Status == 'rebuild') {
                        echo 'Recreate Snappass service'
                        sh "docker-compose up -d --force-recreate --remove-orphans"
                    } else {
                        echo 'Stop Snappass service'
                        sh "docker-compose down"
                    }
                }
            }
        }
    }
    post {
        success {
            echo 'Successful!!!!'
        }
        failure {
            echo 'Failed!!!!!'
        }
        changed {
            echo 'Was some changes!!!!'
        }
    }
}
