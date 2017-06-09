pipeline {
    agent any
	tools { 
        	maven 'Maven 3.3.9' 
        	jdk 'jdk8' 
   	      }
	
	stages {
        stage ('Initialize') {
            steps {
               sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                ''' 
                  }
                             }
        
	stage ('Build') {
            steps {
                sh '''
			mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
			cd /var/lib/jenkins/workspace/My\ Java\ Project/my-app
			mvn package
		'''
            }
            post {
                success {
                    junit 'target/surefire-reports/**/*.xml' 
                }
        }
}
}
}
    

