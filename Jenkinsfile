pipeline 
{
  agent any
  
  stages 
  {
    stage('Build') 
    {
      steps 
      {
        dir(path: 'maven') 
        {
          withMaven(maven: 'Maven 3.5.0') 
          {
            sh 'mvn package -Dmaven.test.failure.ignore'
          }
        }
      }
    }
    
    stage('Document') 
    {
      steps 
      {
        dir(path: 'maven') 
        {
          withMaven(maven: 'Maven 3.5.0') 
          {
            sh 'mvn site:site'
          }
        }
      }
    }
    
    stage('Analyze') 
    {
      when
      {
      	expression {return currentBuild.result == "STABLE"}
      }
      steps 
      {
        echo 'Perform code analysis here.'
      }
    }
    
    stage('Deploy') 
    {
      steps 
      {
        echo 'Perform automated deployment here.'
      }
    }
    
    stage('Test') 
    {
      steps 
      {
        echo 'Perform automated functional tests here.'
      }
    }
  }
  
  post
  {
  	unstable
  	{
  		echo 'Unit tests failed.'
  	}
  }
}
