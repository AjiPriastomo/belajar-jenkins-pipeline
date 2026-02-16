pipeline {
    agent {
        node {
            label "windows || java17"
        }
    }
    stages {
        stage("Hello"){
            steps {
                echo("hello pipeline")
            }
        }
    }

    post {
        always {
            echo " Pipeline always send this message "
        }
        success {
            echo " Pipeline is success "
        }
        failure {
            echo " Pipeline is failure "
        }
        cleanup {
            echo " cleanup is running "
        }
    }
}


