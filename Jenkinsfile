pipeline {
    agent any

    parameters{
        string(name:"tomcat_dev",defaultValue:'jenkins-master',description:'Staging Server')
        string(name:"tomcat_prod",defaultValue:'jenkins-master',description:'Production Server')
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
                    sh "scp /var/lib/jenkins/workspace/PipelineAsCodeExample/webapp/target/*.war shady@jenkins-master:/var/lib/tomcat8/webapps "
                }
            }
        
    }
    
}
