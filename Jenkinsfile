pipeline {
    agent any

    parameters{
        string(name:"tomcat_dev",defaultValue:'10.64.106.246',description:'Staging Server')
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
                    sh "scp -i ${JENKINS_HOME}/tomcat-demo.pem **/target/*.war shady@${env.tomcat_dev}:/var/lib/tomcat8/webapps "
                }
            }
        
    }
    
}
