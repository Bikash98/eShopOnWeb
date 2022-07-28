pipeline {
agent any
     options {
        timestamps()
    }
    stages {  

        stage ("Clone Repository") {
                steps {
                   git branch: 'main', url: 'https://github.com/Bikash98/eShopOnWeb.git'
                }
            }  
        stage('Prep') {
            steps {
                script {
                    GIT_BRANCH=sh(returnStdout: true, script: 'git symbolic-ref --short HEAD').trim()
                    currentBuild.setDisplayName("#${currentBuild.number} [" + GIT_BRANCH + "]")
                    sh "export GIT_BRANCH=$GIT_BRANCH"
                }
            }
        }  
        stage ('Building dll') {
            steps {
               sh "dotnet build eShopOnWeb.sln"
            }           
        }
        /////stage ('Copy proj to backup') {
            steps {
                script {
                    echo "Copying project folder to backup folder"
                    sh "cp -r ${project_folder} ${backup_folder}/${JOB_NAME}_${currentBuild.number}"
                }
            }
        }
        stage('Quality Analysis') {
            parallel {
                // run Sonar Scan and Integration tests in parallel.
                stage('Integration Test') {
                    steps {
                        echo 'Run integration tests here...'
                    }
                }
        stage ('Declarative Post Options') {
            steps {
                script {
                    echo 'Sending Post Build Notifications'
                }
            }  
            }
    }
}
    }
}
