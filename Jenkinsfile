pipeline {
    agent { label 'jworker' }

    environment{
        old_files = fileExists './output'
        old_containers = sh 'docker ps -a |grep "cura-build"'
    }

    stages {
        
        stage ('Clean environment files') {            

            when { expression { old_files == 'true' } }
            steps {
                sh 'sudo rm -r ./output'
            }
        }

        stage ('Clean environment docker') {            

            when { expression { old_containers == 'true' } }
            steps {
                sh 'docker stop cura-build'
                sh 'docker rm cura-build'
                sh 'docker image rm 8b25c9f4b47a'
            }
        }        
/*
        stage ('Run build') {
            steps {
                sh 'sudo ./docker/linux/build.sh'
            }
        }
*/
    }
}