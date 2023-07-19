pipeline {
    agent any

    triggers {
        cron('H 0 * * *') // This schedules the job to run daily at midnight
    }

    stages {

        stage("Cleanup Workspace"){
            steps {
                cleanWs()
            }
        }
        
        stage("Checkout from SCM"){
            steps {
                git branch: 'master', credentialsId: 'deploy', url: 'https://github.com/DevBarham/testing-apps-with-rtl'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh '''
                        
                        npm install
                    '''
                }
                
            }
        }

        stage('Test') {
            steps {
                script{
                    echo "Test App..."
                    sh '''
                        npm run test

                    '''

                }
            }
        }

        stage('Deploy') {
            steps {
                script{
                 echo 'Deploying App...'
                    sh ''' 
                    npm run start
                    '''
                    sh '''
                     sh 'sudo cp -r dist/* /var/www/html' // Copy build files to NGINX directory
                    sh 'sudo systemctl restart nginx' // Restart NGINX to apply changes
                    '''
                }
            }
        }
    }

}








// pipeline {
//     agent any

//     triggers {
//         cron('H 0 * * *') // This schedules the job to run daily at midnight
//     }

//     stages {
//         stage('Checkout') {
//             steps {
//                 cleanWs() // Clean workspace before checking out the code
//                 git branch: 'main', credentialsId: 'deploy', url: 'https://github.com/DevBarham/Nodejs-app-periodic-deployment-jenkins-cicd'
//                 checkout scm
//             }
//         }

//         stage('Install Dependencies') {
//             steps {
//                 dir('Nodejs-app-periodic-deployment-jenkins-cicd/client-side'){
//                 script{
//                        sh 'ls'
//                     //    sh 'cd client-side ls'
                       
//                 }}}}}} 

// //                     sh 'cd client-side' // Use "npm ci" for a clean install of dependencies
// //                     sh 'npm i'
// //                     sh 'cd server-side'
// //                     sh 'npm i'
// //                 }
                
// //             }
// //         }

// //         stage('Test') {
// //             steps {
// //                 script{
// //                  // Run tests
// //                 sh 'cd server-side'
// //                 sh 'npm test'

// //                 }
// //             }
// //             post {
// //                 success {
// //                     echo 'Tests passed. Proceeding with the build...'
// //                 }
// //                 failure {
// //                     echo 'Tests failed. Aborting the build.'
// //                     error 'Tests failed.'
// //                 }
// //             }
// //         }

// //         stage('Build') {
// //             steps {
// //                 script{
// //                 sh 'cd client-side'
// //                 sh 'npm run build' // Add your build commands here
// //                 sh 'cd server-side'
// //                 sh 'npm start'

// //                 }
// //             }
// //         }

// //         stage('Deploy') {
// //             steps {
// //                 // Add deployment steps here
// //                  echo 'Deploying App...'
// //             }
// //         }
// //     }

// //     post {
// //         always {
// //             // Clean up or perform any post-build actions here
// //              echo 'Performing post-build actions...'
// //         }
// //         success {
// //             echo 'Build and deployment were successful.'
// //         }
// //         failure {
// //             echo 'Build or deployment failed.'
// //             error 'Build or deployment failed.'
// //         }
// //     }
// // }
