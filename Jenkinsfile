pipeline {
    agent any
    
    stages {
        stage("checkout") {
            steps {
                sh "ls"
                git branch: 'main', url: 'https://github.com/jorgechb/course3-jenkins-gs-spring-petclinic'
                sh "ls"  
            }
        }
        
        stage("build") {
            steps {
                sh "./mvnw package"
            }
        }
        
        stage("capture") {
            steps {
                archiveArtifacts '**/target/*.jar'
                jacoco()
                junit '**/target/surefire-reports/TEST*.xml' 
            }
            
        }
    }
    
    post {
        always {
            mail body: "${env.BUILD_URL}\\n${currentBuild.absoluteUrl}", 
                subject: "${currentBuild.currentResult}: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]", 
                to: 'jch.waldo@gmail.com'
        }
    }
}