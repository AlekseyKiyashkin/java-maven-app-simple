pipeline {
    agent any
    tools {
        maven 'maven-3.9.3'
    }

    stages {
   
        stage("build jar") {
            steps {
                script {
                    echo "building the application..."
                    sh 'mvn package'
                }
            }
        }

        stage("build image") {
            steps {
                script {
                    echo 'building the docker image...'
                    withCredentials ([usernamePassword(credentialsId:'6ec9d130-1d94-42af-9cf5-26ab651d58da', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh ''' 
                        docker build . -t kryssperer/nanasapp:1.5
                        echo $PASS | docker login -u $USER --password-stdin
                        docker push kryssperer/nanasapp:1.5
                        '''
                    }

                }
            }
        }

        stage("deploy") {
            steps {
                echo "deploying the application ..."
            }
        }
    }

}