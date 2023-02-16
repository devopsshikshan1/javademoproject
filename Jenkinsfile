pipeline {
    agent any
     tools{
         maven 'maven 3.8.7'
     }
    stages {
        stage('CodeChecoout') {
            steps {
            git 'https://github.com/devopsshikshan1/javademoproject.git'
            }
        }
        stage('BuildArtifacts') {
            steps {
            sh 'mvn clean package'
            }
        }
        stage('CodeQualityCheck'){
        steps{
        sh '''mvn clean verify sonar:sonar \\
  -Dsonar.projectKey=pipeline_01 \\
  -Dsonar.host.url=http://13.234.232.170:9000/ \\
  -Dsonar.login=sqp_2aa6b6cd26f7fa4f8ba9cf18e73723dc94dbee26'''
        }
    }    
      stage('deployWarToTomcat'){
                steps{
                    deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://13.232.68.73:8080/')], contextPath: 'javawebapplication', war: '**/*.war'
                     }
      }
    }
}
