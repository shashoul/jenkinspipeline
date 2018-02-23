pipeline {
    agent any

    stages{
        stage('Build'){
            steps{
                sh "mvn clean package"
            }
            post{
                success{
                    echo "Archiving..."
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        
            stage('Deploy to staging'){
                steps{
                    sh "scp -i /var/lib/jenkins/id_rsa.pub /var/lib/jenkins/workspace/PipelineAsCodeExample/webapp/target/*.war shady@jenkins-master:/var/lib/tomcat8/webapps "
                }
            }
        
    }
    
}
