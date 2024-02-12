pipeline{
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage ('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to tomcat server') {
            steps{
                script{
                    readProp = readProperties file: 'build.properties'
                }
               deploy adapters: [tomcat9(credentialsId: 'tomcat_deployer', path: '', url: 'http://localhost:8090')], contextPath: null, war: '**/*.war' echo "This is running on ${readProp['deploy.type']}"
               
            }
        }
    }
}
