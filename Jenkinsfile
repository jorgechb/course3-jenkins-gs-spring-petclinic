pipeline {
    agent any
     
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