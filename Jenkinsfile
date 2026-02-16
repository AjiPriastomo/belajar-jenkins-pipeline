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
            }
            steps {
                echo("Build 2")
            }
            steps {
                echo("Build 3")
            }
        }
        stage("Test"){
            steps {
                echo("Test 1")
            }
            steps {
                echo("Test 2")
            }
            steps {
                echo("Test 3")
            }
        }
        stage("Deploy"){
            steps {
                echo("Deploy 1")
            }
            steps {
                echo("Deploy 2")
            }
            steps {
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




