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

stage('SONARAnalysis') {
       steps {

sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=spring-petclinic \
  -Dsonar.projectName='spring-petclinic' \
  -Dsonar.host.url=http://54.67.112.31:9000 \
  -Dsonar.token=sqp_163f686a74903d9d57a294d6914acb06a65ab016'
         
       }

        
      }
    


    stage('test') {

steps {

echo "testing the code"
  
  
}
      
    }


  
        

        
      
   
    


    stage('Dockerize') {

steps {

echo "dockerizze"
  
}

      
    }

    

    stage('deploy') {

steps {

echo "deploying the code"
  /* # sh 'nohup java -jar target/*.jar & sleep 10' */
  
}

    }

    stage('upload artifact') {

steps {

nexusArtifactUploader(
        nexusVersion: 'nexus3',
        protocol: 'http',
        nexusUrl: '54.219.60.86:8081',
        groupId: 'org.springframework',
  
        version: "2.4.${env.BUILD_NUMBER}",
        repository: 'code-repo',
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
