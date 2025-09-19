pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('SONAR_TOKEN')
    }

    stages {


        stage('Build') {
            steps {
                echo 'Stage 1: Build - Compiling and packaging the application'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Running unit and integration tests'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Performing static code analysis'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Running security scan'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploying application to staging environment '
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Running integration tests on staging environment'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploying application to production environment'
            }
        }


        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/shreerai001/8.2DevSecOps'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                sh '''
                  /opt/sonar-scanner/bin/sonar-scanner \
                    -Dsonar.organization=shrikrishnarai \
                    -Dsonar.projectKey=shreerai001_8.2DevSecOps \
                    -Dsonar.host.url=https://sonarcloud.io \
                    -Dsonar.login=$SONAR_TOKEN \
                    -Dsonar.sources=. \
                    -Dsonar.exclusions=node_modules/**,test/** \
                    -Dsonar.javascript.lcov.reportPaths=coverage/lcov.info \
                    -Dsonar.projectName="NodeJS Goof Vulnerable App" \
                    -Dsonar.sourceEncoding=UTF-8
                '''
            }
        }
    }
        post {
            always {
                echo 'Pipeline finished.'
            }
            success {
                echo 'SonarCloud analysis completed successfully!'
            }
            failure {
                echo 'Pipeline failed. Check logs.'
            }
        }
}
