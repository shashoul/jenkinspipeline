pipeline {
    agent any

    parameters{
        string(name:"tomcat_dev",defaultValu:'jenkins-master',description:'Staging Server')
        string(name:"tomcat_prod",defaultValu:'jenkins-master',description:'Production Server')
    }
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
                    sh "scp -i /home/shady/.ssh/id_rsa.pub /var/lib/jenkins/workspace/PipelineAsCodeExample/webapp/target/*.war shady@${params.tomcat_dev}:/var/lib/tomcat8/webapps "
                }
            }
        
    }
    
}
