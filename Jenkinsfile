pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {
        stage('Git Checkout') {
            steps {
                checkout scmGit(
                    branches: [[name: '*/main']],
                    extensions: [],
                    userRemoteConfigs: [[url: 'https://github.com/achrafaboulakjam/sonar']]
                )
                echo 'Git Checkout Completed'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQubeDockerDemo') {
                    bat '''
                        mvn clean verify sonar:sonar \
                        -Dsonar.projectKey=SonarQubeDockerDemo \
                        -Dsonar.host.url=http://13.37.216.213:9001 \
                        -Dsonar.login=sqp_75d4c7e1fdf7afb76d83dddd187e0c76c4d1d2da
                    '''
                    // port 9000 is default for SonarQube
                    echo 'SonarQube Analysis Completed'
                }
            }
        }
    }
}
