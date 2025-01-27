pipeline {
    agent any

    stages {

        stage('approval') {
            steps {
                timeout(time: 60, unit: 'SECONDS') {
                    input message: 'Do you wish to deploy tp production ?', ok: 'Yes ,I am sure!'
            }
                }
                
        }
        stage('hello') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo 'small change'
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }

        // stage('Test')
        // {
        //     agent {
        //         docker {
        //             image 'node:18-alpine'
        //             reuseNode true
        //         }
        //     }
        //     steps{
        //         sh '''
        //             test -f build/index.html
        //             npm test 
        //         '''
        //     }
        // }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }

}
