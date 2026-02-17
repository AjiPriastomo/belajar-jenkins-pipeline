pipeline {
    agent none
    environment {
        AUTHOR = "Aji Priastomo"
        CRED = credentials("aji-cred")
    }
    stages {
        stage("Prepare"){
            agent {
                node {
                    label "local"
                }
            }
            steps {
                echo("Author : ${AUTHOR}")
                echo("Start Job : ${env.JOB_NAME}")
                echo("Start Build : ${env.BUILD_NUMBER}")
                echo("Branch Name : ${env.BRANCH_NAME}")
                echo("App User : ${CRED_USR}")
                echo("App Pass : ${CRED_PSW}")
            }
        }
        stage("Build"){
            agent {
                node {
                    label "local"
                }
            }
            steps {
                echo("Start Build")
                bat("mvn clean compile test-compile")
                echo("Finish Build")
            }
        }
        stage("Test"){
            agent {
                node {
                    label "local"
                }
            }
            steps {
                script {
                    def data = [
                        "firstName" : "Aji",
                        "lastName" : "Priastomo"
                    ]
                    writeJSON(file: "data.json", json: data)
                }
                echo("Test 1")
                bat("mvn test")
                echo("Test 3")
            }
        }
        stage("Deploy"){
            agent {
                node {
                    label "local"
                }
            }
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













