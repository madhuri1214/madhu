pipeline {
   agent any
	environment {

      sonar_url = 'http://172.31.12.54:9000/'
      sonar_username = 'admin'
      sonar_password = 'password123'
      nexusUrl = '172.31.12.54:8081'
      artifact_version = '0.0.1'

 }
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
           clean install
           '''
         }
	}
	   stage ('Sonarqube Analysis'){
           steps {
           withSonarQubeEnv('sonarqube') {
           sh '''
           mvn clean package org.jacoco:jacoco-maven-plugin:prepare-agent install -Dmaven.test.failure.ignore=false
           mvn -e -B sonar:sonar -Dsonar.java.source=1.8 -Dsonar.host.url="${sonar_url}" -Dsonar.login="${sonar_username}" -Dsonar.password="${sonar_password}" -Dsonar.sourceEncoding=UTF-8
           '''
           }
         }
      }
      }
	}
