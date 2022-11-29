pipeline {
    agent none
    
    parameters{
         string defaultValue: 'debian', description: 'Nombre del Nodo  del ambiente QA,   ', name: 'LABEL_QA_NODE', trim: false
         string defaultValue: 'debian', description: 'Nombre del Nodo  del ambiente PROD,   ', name: 'LABEL_PROD_NODE', trim: false
         string defaultValue: 'debian', description: 'Nombre del Nodo  del ambiente DEV,   ', name: 'LABEL_DEV_NODE', trim: false

     }
    environment{
        QA_NODE="${params.LABEL_QA_NODE}"
        PROD_NODE="${params.LABEL_PROD_NODE}"
        DEV_NODE="${params.LABEL_DEV_NODE}"
    }

    stages {
        stage('cloning') {
            agent {label DEV_NODE}
            steps {
                dir('backend'){
                    git 'https://github.com/RodrigoCoronelLoza/MusicShopDjango.git'
                }
                dir('frontend'){
                    git 'https://github.com/RodrigoCoronelLoza/module8lab5.git'
                }
                sh "echo DEV!"
            }    
        }
        stage('build'){
            agent {label DEV_NODE}
            steps{
                sh "docker-compose build"
                sh "docker-compose up -d"
                sh "docker-compose ps"
                sh "echo DEV!"
            }
        }
        
        stage('QA'){
            agent {label QA_NODE}
            steps{
                //sh "docker-compose build"
                sh "echo QA!"
            }
        }
        
        stage('PROD'){
            agent {label PROD_NODE}
            steps{
                //sh "docker-compose build"
                sh "echo PROD!"
            }
        }
    }
}
