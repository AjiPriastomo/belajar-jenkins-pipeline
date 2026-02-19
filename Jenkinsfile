pipeline {
    agent none
    environment {
        AUTHOR = "Aji Priastomo"
        CRED = credentials("aji-cred")
    }
    parameters {
        string(name:"NAME", defaultValue :"Guest", description: "what is your name ?" )
        text(name:"DESCRIPTION", defaultValue :"Guest", description: "Tell me about you" )
        booleanParam(name:"DEPLOY", defaultValue : false, description: "Need to deploy ?" )
        choice(name:"SOCIAL_MEDIA", choices : ['Intagram', 'Facebook'], description: "Which Social Media" )
        password(name:"SECRET", defaultValue :"Guest", description: "Encrypt Key" )
    }
    //triggers {
        //cron(" */10 * * * *")
    //}
    options {
        disableConcurrentBuilds()
        timeout(time: 10, unit : 'MINUTES')
    }
    stages {
        stage("OS Setup"){
            matrix{
                axes{
                    axis{
                        name "OS"
                        values "Linux", "Windows", "Mac"
                    }
                    axis{
                        name "Arc"
                        values "32", "64"
                    }
                }
            }

            stages {
                stage("OS Setup"){
                    agent {
                        node {
                            label "local"
                        }
                    }
                }
                steps{
                    echo("setup : ${OS} ${Arc}")
                }
            }
        }
        stage("Preparation"){
            failFast true
            parallel {
                stage("Preper java"){
                    agent {
                        node {
                            label "local"
                        }
                    }
                    steps {
                        echo("Prepare java")
                        sleep(5)
                    }
                }
                stage("Preper Maven"){
                    agent {
                        node {
                            label "local"
                        }
                    }
                    steps {
                        echo("Prepare Maven")
                        sleep(5)
                    }
                }
            }
        }
        stage("Parameter"){
            agent {
                node {
                    label "local"
                }
            }
            steps {
                echo "Hello : ${params.NAME}"
                echo "your description : ${params.DESCRIPTION}"
                echo "Your Social media : ${params.SOCIAL_MEDIA}"
                echo "Need to Deploy : ${params.DEPLOY}"
                echo "Your Secret : ${params.SECRET}"
            }
        }
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
                bat("echo 'App Password : $CRED_PSW' > 'rahasia.txt'")
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
            input {
                message "can we deploy ?"
                ok "Yes, of course"
                submitter "Jamal"
                parameters {
                    choice(name:"TARGET_ENV", choices : ['DEV', 'QA', 'PROD'], description: "Which Environment ?" )
                }
            }
            agent {
                node {
                    label "local"
                }
            }
            steps {
                echo("Deploy in ${TARGET_ENV}")
    
            }
        }
        stage("Release"){
            when {
                expression{
                    return params.DEPLOY
                }
            }
            agent {
                node {
                    label "local"
                }
            }
            steps {
                echo("Release it")
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
































