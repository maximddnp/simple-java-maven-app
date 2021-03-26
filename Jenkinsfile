pipeline {
    agent {
        kubernetes {
            yamlFile 'build-pod.yaml'
        }
    }
    stages {
        stage('Run maven') {
            steps {
                container('maven') {
                    sh 'mvn -B clean install'
                }
                container('docker') {
                    sh 'docker version && DOCKER_BUILDKIT=1 docker build --progress plain -t testing .'
                }
            }
        }
    }
}





//podTemplate(containers: [
//        containerTemplate(name: 'maven', image: 'maven:3.3.9-jdk-8-alpine', ttyEnabled: true, command: 'cat'),
//        containerTemplate(name: 'golang', image: 'golang:1.8.0', ttyEnabled: true, command: 'cat')
//]) {
//
//    node(POD_LABEL) {
//        stage('Checkout') {
//            steps {
//                checkout scm
//            }
//        }
//        stage('Get a Maven project') {
//            container('maven') {
//                stage('Build a Maven project') {
//                    sh 'mvn -B clean install'
//                }
//            }
//        }
//
//        stage('Docker build') {
//            container('docker') {
//                stage('Build docker image') {
//                    sh 'docker version && DOCKER_BUILDKIT=1 docker build --progress plain -t testing .'
//                }
//            }
//        }
//
//    }
//}






//pipeline {
//    agent {
//        kubernetes {
//            label 'test-app'  // all your pods will be named with this prefix, followed by a unique id
//            idleMinutes 5  // how long the pod will live after no jobs have run on it
//            yamlFile 'build-pod.yaml'  // path to the pod definition relative to the root of our project
//            defaultContainer 'maven'  // define a default container if more than a few stages use it, will default to jnlp container
//        }
//    }
//    stages {
//        stage('Build') {
//            steps {  // no container directive is needed as the maven container is the default
//                sh "mvn clean install"
//            }
//        }
//        stage('Build Docker Image') {
//            steps {
//                container('docker') {
//                    sh "docker build -t vividseats/promo-app:dev ."  // when we run docker in this step, we're running it via a shell on the docker build-pod container,
//                    sh "docker push vividseats/promo-app:dev"        // which is just connecting to the host docker deaemon
//                }
//            }
//        }
//    }
//}