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
		sh 'mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false'	
		sh 'mvn -f my-app/pom.xml package'	
            }
            post {
                success {
                    junit 'my-app/target/surefire-reports/*.xml' 
                }
        }
}

	stage ('deploy'){

	steps {
		sh "sudo mkdir -p /var/www/html/all/${env.BRANCH_NAME}"
		sh "sudo cp my-app/target/my-app-1.0-SNAPSHOT.jar /var/www/html/all/${env.BRANCH_NAME}/"
	
	
}
}

	stage ('Promote Development branch to master') {
		when {

			branch 'development'
	
		}
		steps {

		echo "stashing any local changes"
		sh 'git stash'
		echo "checking out development branch"
		sh 'git checkout development'
		echo "checking out master branch"
		sh 'git checkout master'
		echo "Merging development into master branch"
		sh 'git merge development'
		echo "pushing to master branch"
		sh 'git push origin master'
		}
	
	}
}
}
    

