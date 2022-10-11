 pipeline{
    agent any
    
    stages {
        stage('build-env') {
            steps {
                sh '''apt-get update
                apt-get install build-essential -y
                gcc --version
                apt install sloccount'''
            }
        }

        stage('build-hello-world') {
            steps {
                sh 'make clean'
                sh 'make main'
                sh '(ls HelloWorld >> /dev/null 2>&1  && echo yes && exit 0) || echo no || exit 1'
                archiveArtifacts artifacts: '*', followSymlinks: false
            }
        }
    }
    post {
        success {
            triggers {
                upstream 'job 2,'
            }
        }
    }
 }