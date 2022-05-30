pipeline {
   agent any
   stages
   {
   stage('git clone') {
         steps {
            // Get some code from a GitHub repository
            git 'https://github.com/snehitha-reddy/Game.git'
        }  
        }
	stage ('Compile and Build') {
         steps {
           sh '''
           mvn clean install package
           '''
         }
	}
      }
	}
