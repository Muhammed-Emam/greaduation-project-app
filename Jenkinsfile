pipeline {
    agent {
        label 'slave-node'
    }

    stages {

        stage('Build-docker-img') {
            steps {
                script{
                    sh 'docker build -f Dockerfile -t muhammedemam/wep-app .'
                }
            }
        }

        stage('push-docker-img') {
            steps {
                script{
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                        sh "docker login -u muhammedemam -p ${dockerhubpwd}"
                    }
                    sh 'docker push muhammedemam/wep-app'
                }
            }
        }

        stage('cd') {
            steps {
                script{
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                        sh "docker login -u muhammedemam -p ${dockerhubpwd}"
                    }
                    sh """
                    kubectl delete deployment --all -n web-app
                    kubectl apply -f namespace.yaml
                    kubectl apply -f deployment.yaml
                    kubectl apply -f service.yaml

                    """
                }
            }
        }

        

        
    }
}






// pipeline {
//     agent {
//         label 'slave-node'
//     }

//     stages {

//         stage('Build-docker-img') {
//             steps {
//                 withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'DOCKERPASS', usernameVariable: 'DOCKERENAME')]) {
//                     sh """ 
//                     docker build . -t muhammedemam/wep-app
//                     docker login -u ${DOCKERENAME} -p ${DOCKERPASS}
//                     docker push muhammedemam/wep-app
//                     """
//                 }
//             }
//         }


//         stage('cd') {
//             steps {
//                 withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'DOCKERPASS', usernameVariable: 'DOCKERENAME')]) {
//                     sh """
//                     docker login -u ${DOCKERENAME} -p ${DOCKERPASS}
//                     kubectl delete deployment --all -n simple-web
//                     kubectl apply -f namespace.yaml
//                     kubectl apply -f deployment.yaml
//                     kubectl apply -f service.yaml
//                     """
//                 }
//             }
//         }
//     }
// }