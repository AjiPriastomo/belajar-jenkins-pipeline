pipeline {
    agent {
        node {
            label "local"
        }
    }
    stages {
        stage("Build"){
            steps {
                echo("Build 1")
                echo("Build 2")
                echo("Build 3")
            }
        }
        stage("Test"){
            steps {
                echo("Test 1")
                echo("Test 2")
                echo("Test 3")
            }
        }
        stage("Deploy"){
            steps {
                echo("Deploy 1")
                echo("Deploy 2")
                echo("Deploy 3")
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





