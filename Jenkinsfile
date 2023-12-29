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

    }
 
    


    
  }




  
}
