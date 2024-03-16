pipeline {
    agent { label "Helloworld_project" }
    
    triggers {
        pollSCM('* * * * *')
    }    

    stages {
        stage('clone_Helloworld_project') {
            steps {
                echo 'Helloworld_project'
                git 'https://github.com/harishtg1234/Helloworld_project.git'
            }
        }
        stage('build_Helloworld_project') {
            steps {
                echo 'build_Helloworld_project'
                sh 'yum install maven -y'
                sh 'mvn -Dmaven.test.failure.ignore=true install'
            }
        } 
        stage('Docker_build') {
            steps {
                echo 'Docker build_Helloworld_project'
                sh 'docker build -t Helloworld_project .' 
            }
        }
        stage('login to dockerhub') {
            steps {
                echo 'login to dockerhub'
                sh 'docker login -u harishtg1234 -p dockerhub@2618'
            }
        } 
        stage('Tag the Image') {
            steps {
                echo 'Tag the Image'
                sh 'docker tag  Helloworld_project harishtg1234/Helloworld_project'
            }
        } 
        stage('Deploy to docker hub') {
            steps {
                echo 'Deploy to docker hub'
                sh 'docker push harishtg1234/Helloworld_project'
            }
        }
        stage('Remove Docker conatiner') {
            steps {
                echo 'Remove Docker conatiner'
                sh 'docker stop Helloworld_project_conatiner || true'
                sh 'docker rm Helloworld_project_conatiner || true'
            }
        }        
        stage('Run docker image') {
            steps {
                echo 'Deploy to docker hub'
                sh 'docker run --name Helloworld_project_conatiner -d -p 80:80:8080 harishtg1234/Helloworld_project'
            }
        }
        stage('added one more stage') {
            steps {
                echo 'added one more stage'                
            }
        }        
    }
}
