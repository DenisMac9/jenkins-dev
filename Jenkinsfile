pipeline {

    agent {
	    label "autoscale"
    }

    triggers {
        pollSCM('*/1 * * * *')
    }
    
    options { disableConcurrentBuilds() }

    environment {
        REGISTRY_AUTH_USR = credentials("docker-registry-user")
        REGISTRY_AUTH_PSW = credentials("docker-registry-password")
    
        BUILD_NUMBER = "${env.BUILD_NUMBER}"
        BRANCH_NAME = "${env.BRANCH_NAME}"
    }

    stages {

        stage ('Checkout') {
            steps {
                checkout scm
            }
        }

        stage ('Docker Build Images') {
            steps {
                sh 'docker build -t denismac9/vote:$BRANCH_NAME vote'
                sh 'docker build -t denismac9/result:$BRANCH_NAME result'

                sh "docker login -u=$REGISTRY_AUTH_USR -p=$REGISTRY_AUTH_PSW"
                sh 'docker push denismac9/vote:$BRANCH_NAME'
                sh 'docker push denismac9/result:$BRANCH_NAME'
            }
        }

    }
}

