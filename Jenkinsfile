/*
pipewithAWS(profile:'Test Publisher') {
    s3Upload( file:'ok.txt', bucket:'my-buckeck', path:'file.txt')

}
*/


pipeline {
    agent {
        kubernetes {
            label 'my-pod-template'
            defaultContainer 'jnlp'
            yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: some-label-value
spec:
  containers:
  - name: maven
    image: maven:alpine
    command:
    - cat
    tty: true
  - name: busybox
    image: busybox
    command:
    - cat
    tty: true
"""
        }
    }
    stages {
        stage('Run maven') {
            steps {
                container('maven') {
                    sh 'mvn -version'
                    withAWS(region: 'eu-west-1'){
                    s3Upload( file:'Jenkinsfile', bucket:'stu-cje-backups', path:'Jenkinsfile')
                    }
                }
            }
        }
    }
}
