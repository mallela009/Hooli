pipeline{
    agent any
    tools{
        maven 'MAVEN_HOME'
    }
    stages{
        stage('Checkout'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'githubtoken', url: 'https://github.com/mallela009/Hooli.git']]])
            }
        }
        stage('Build'){
            steps{
           sh 'mvn clean package'
            }
        }
        stage('compile'){
            steps{
             sh 'mvn compile'
            }
        }
    }
        post{
            always{
                echo "archieve the artifacts"
                archieveArtifacts artifacts: '**/target/*.war'
            }
        }
        stage('Deploy to tomcat server'){
            steps{
               deploy adapters: [tomcat9(credentialsId: 'tomcat9', path: '', url: 'http://192.168.1.33:8081/')], contextPath: null, war: '**/*.war' 
               
               
         }
        }
    }

