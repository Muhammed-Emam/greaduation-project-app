// pipeline {
//     agent {
//         label 'slave'
//     }


//     environment {
//         imageName = "node-app"
//         registryCredentials = "nexus"
//         registry = "http://34.29.26.163:8081/repository/docker-private-registry/"
//         dockerImage = ''
//     }


//     stages {
//         stage('Clone Repository') {
//             steps {
//                 // Clone the repository
//                 git url: 'https://github.com/Muhammed-Emam/greaduation-project-app.git', branch: 'main'
//             }
//         }

//         // stage('Build Image') {
//         //     steps {
//         //         // // Build the image as per your requirements
//         //         sh 'docker build -t node-app:latest .'
//         //     }
//         // }

//         stage('Push to Nexus') {
//             steps {
//                 // Login to the Nexus registry
                
//                 withCredentials([usernamePassword(credentialsId: 'nexus', passwordVariable: 'pass', usernameVariable: 'user')]) {
//                     sh "docker login 10.52.9.95:8085 -u $user -p $pass 
//                     sh 'docker build -t node-app:latest .'
//                 }

            
//         }

//         // stage('Deploy Image') {
//         //     steps {
//         //         // Deploy the app from the Nexus registry to the Cluster
//         //         sh '''
//         //         kubectl apply -f myapp.yaml
//         //         kubectl apply -f mysql.yaml
//         //         '''
//         //     }
//         // }
//     }
// }





// // pipeline {
// //     agent {
// //         label 'slave-node'
// //     }

// //     stages {

// //         stage('Build-docker-img') {
// //             steps {
// //                 script{
// //                     sh 'docker build -f Dockerfile -t muhammedemam/wep-app .'
// //                 }
// //             }
// //         }

// //         stage('push-docker-img') {
// //             steps {
// //                 script{
// //                     withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
// //                         sh "docker login -u muhammedemam -p ${dockerhubpwd}"
// //                     }
// //                     sh 'docker push muhammedemam/wep-app'
// //                 }
// //             }
// //         }

// //         stage('cd') {
// //             steps {
// //                 script{
// //                     withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
// //                         sh "docker login -u muhammedemam -p ${dockerhubpwd}"
// //                     }
// //                     sh """
// //                     kubectl delete deployment --all -n web-app
// //                     kubectl apply -f namespace.yaml
// //                     kubectl apply -f deployment.yaml
// //                     kubectl apply -f service.yaml

// //                     """
// //                 }
// //             }





// //         }

        

        
// //     }
// // }



 







// // // pipeline {
// // //     agent {
// // //         label 'slave-node'
// // //     }

// // //     stages {

// // //         stage('Build-docker-img') {
// // //             steps {
// // //                 withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'DOCKERPASS', usernameVariable: 'DOCKERENAME')]) {
// // //                     sh """ 
// // //                     docker build . -t muhammedemam/wep-app
// // //                     docker login -u ${DOCKERENAME} -p ${DOCKERPASS}
// // //                     docker push muhammedemam/wep-app
// // //                     """
// // //                 }
// // //             }
// // //         }


// // //         stage('cd') {
// // //             steps {
// // //                 withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'DOCKERPASS', usernameVariable: 'DOCKERENAME')]) {
// // //                     sh """
// // //                     docker login -u ${DOCKERENAME} -p ${DOCKERPASS}
// // //                     kubectl delete deployment --all -n simple-web
// // //                     kubectl apply -f namespace.yaml
// // //                     kubectl apply -f deployment.yaml
// // //                     kubectl apply -f service.yaml
// // //                     """
// // //                 }
// // //             }
// // //         }
// // //     }
// // // }




// pipeline {
//     agent {
//         label 'slave'
//     }
//     stages {
//         stage ('CI') {
//             steps {
//                 withCredentials([usernamePassword(credentialsId: 'nexus', passwordVariable: 'pass', usernameVariable: 'user')]) {
//                     sh "docker login 10.52.9.95:8085 -u ${user} -p ${pass}

//             }
//         }
//     }
// }

pipeline{
    agent {
        label 'slave'
    }

    stages {
      
        stage("CI"){
            steps {
                withCredentials([usernamePassword(credentialsId: 'nexus',usernameVariable: 'user',passwordVariable: 'pass')]){
                  sh 'docker build -t 35.222.79.122:8085/repository/docker-repo/node-app:latest .'
                  sh 'docker login 35.222.79.122:8085 -u ${user}  -p ${pass}'
                  sh 'docker push 35.222.79.122:8085/repository/docker-repo/node-app:latest'
                }
            }
        }
        stage("CD") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'nexus',usernameVariable: 'user',passwordVariable: 'pass')]){
                  sh 'kubectl create secret docker-registry regcred   --namespace=dev   --docker-server=35.222.79.122:8085   --docker-username=${user}   --docker-password=${pass}   --docker-email=admin@example.org'
                  sh 'docker login 35.222.79.122:8085 -u ${user}  -p ${pass}'
                  sh 'kubectl apply -f configmap.yaml'
                  sh 'kubectl apply -f deployment.yaml'
                  sh 'kubectl apply -f svc.yaml '
                }
            }   
        }
    }
}