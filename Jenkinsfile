pipeline {


agent any

  stages {

stage('git clone') {

  steps {

echo "cloning the code repo from github"
git branch: 'main', url: 'https://github.com/BecomeDevops/spring-petclinic.git'
    
  }

  
}

    stage('Build') {
   steps {
    echo "build the code and creating a jar file"
    sh './mvnw package' 

     
   }

      
    }


    stage('test') {

steps {

echo "testing the code"
  
}
      
    }

    stage('deploy') {

steps {

echo "deploying the code"
  sh 'nohup java -jar target/*.jar & sleep 10'
  
}

 stage('upload artifact') {
        steps {

       nexusArtifactUploader(
        nexusVersion: 'nexus3',
        protocol: 'http',
        nexusUrl: '54.183.5.231:8081',
        groupId: 'org.springframework',
        version: "${env.BUILD_ID}-${env.BUILD_TIMESTAMP}",
        repository: 'jarvisartifactrepo',
        credentialsId: 'nexuslogin',
        artifacts: [
            [artifactId: spring-petclinic,
             classifier: '',
             file: 'target/*.jar',
             type: 'jar']
        ]
     )

      
    }
      }

    


    
  }




  
}
