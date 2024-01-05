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


    stage('sonar analysis') {


      steps {
    withSonarQube('sonarserver') {
sh ''' $SCANNER_HOME/bin/sonarscanner -Dsonar.projectName=spring-petclinic \
-Dsonar.projectKey=spring-petclinic '''

    }
        
        

        
      }
      echo "checking analysis "
    }

    stage('sonar quality gates') {


      steps {
echo "quality gate metrics "
       script {
      

waitForQualityGate abortPipeline: false, credentialsId: 'sonartoken'
         
       }
      }
    }

    

    stage('deploy') {

steps {

echo "deploying the code"
  sh 'nohup java -jar target/*.jar & sleep 10'
  
}

    }

    stage('upload artifact') {

steps {

nexusArtifactUploader(
        nexusVersion: 'nexus3',
        protocol: 'http',
        nexusUrl: '54.219.60.86:8081',
        groupId: 'org.springframework',
        version: '2.4.5',
        repository: 'springproject-repo',
        credentialsId: 'nexuscreds',
        artifacts: [
            [artifactId: 'spring-petclinic',
             classifier: '',
             file: 'target/spring-petclinic-2.4.5.jar',
             type: 'jar']
        ]
     )

  
}

      
    }
 
    


    
  }




  
}
