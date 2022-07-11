node {
    def mavenHome= tool name: "Maven3.8.6"
    stage('Checkout stage')
    {
        git branch: 'development', credentialsId: 'a3d54419-af0b-4295-8532-f4939e69eb8e', 
        url: 'https://github.com/kushalj1990/maven-web-application.git'
    }
    stage('Build stage')
    {
      sh "$mavenHome/bin/mvn clean package"  
    }
    
    stage('Sonarqube report')
    {
        sh "$mavenHome/bin/mvn sonar:sonar"
    }
    
    stage('Upload files to artifacts')
    {
       sh "$mavenHome/bin/mvn deploy"
    }
    
    stage('Upload files to Tomcat')
    {
       sshagent(['370dd5dc-0d01-42b4-bbbe-7442d0d4a45d']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@15.206.157.251:/opt/apache-tomcat-9.0.64/webapps"
} 
    }
}
