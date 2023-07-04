pipeline {
    agent {
        label 'slave'
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the repository
                git url: 'https://github.com/Muhammed-Emam/greaduation-project-app.git', branch: 'main'
            }
        }

        stage('Build Image') {
            steps {
                // Build the image as per your requirements
                sh 'docker build -t node-app:latest .'
            }
        }

        // stage('Push to Nexus') {
        //     steps {
        //         // Login to the Nexus registry
        //         withCredentials([usernamePassword(credentialsId: 'nexus', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
        //             sh "docker login -u $USERNAME -p $PASSWORD 10.103.254.180:5000"
        //         }

        //         // Tag the image with Nexus registry information
        //         sh 'docker tag node-app:latest 10.103.254.180:5000/repository/ahmed-repo/app:latest'

        //         // Push the image to Nexus registry
        //         sh 'docker push 10.103.254.180:5000/repository/ahmed-repo/app:latest'
        //     }
        // }

        // stage('Deploy Image') {
        //     steps {
        //         // Deploy the app from the Nexus registry to the Cluster
        //         sh '''
        //         kubectl apply -f myapp.yaml
        //         kubectl apply -f mysql.yaml
        //         '''
        //     }
        // }
    }
}





// pipeline {
//     agent {
//         label 'slave-node'
//     }

//     stages {

//         stage('Build-docker-img') {
//             steps {
//                 script{
//                     sh 'docker build -f Dockerfile -t muhammedemam/wep-app .'
//                 }
//             }
//         }

//         stage('push-docker-img') {
//             steps {
//                 script{
//                     withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
//                         sh "docker login -u muhammedemam -p ${dockerhubpwd}"
//                     }
//                     sh 'docker push muhammedemam/wep-app'
//                 }
//             }
//         }

//         stage('cd') {
//             steps {
//                 script{
//                     withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
//                         sh "docker login -u muhammedemam -p ${dockerhubpwd}"
//                     }
//                     sh """
//                     kubectl delete deployment --all -n web-app
//                     kubectl apply -f namespace.yaml
//                     kubectl apply -f deployment.yaml
//                     kubectl apply -f service.yaml

//                     """
//                 }
//             }





//         }

        

        
//     }
// }



 







// // pipeline {
// //     agent {
// //         label 'slave-node'
// //     }

// //     stages {

// //         stage('Build-docker-img') {
// //             steps {
// //                 withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'DOCKERPASS', usernameVariable: 'DOCKERENAME')]) {
// //                     sh """ 
// //                     docker build . -t muhammedemam/wep-app
// //                     docker login -u ${DOCKERENAME} -p ${DOCKERPASS}
// //                     docker push muhammedemam/wep-app
// //                     """
// //                 }
// //             }
// //         }


// //         stage('cd') {
// //             steps {
// //                 withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'DOCKERPASS', usernameVariable: 'DOCKERENAME')]) {
// //                     sh """
// //                     docker login -u ${DOCKERENAME} -p ${DOCKERPASS}
// //                     kubectl delete deployment --all -n simple-web
// //                     kubectl apply -f namespace.yaml
// //                     kubectl apply -f deployment.yaml
// //                     kubectl apply -f service.yaml
// //                     """
// //                 }
// //             }
// //         }
// //     }
// // }