pipeline {
   agent any
	environment {

      sonar_url = 'http://172.31.22.66:9000/'
      sonar_username = 'admin'
      sonar_password = 'password123'

 }
	tools {
      // Install the Maven version configured as "M3" and add it to the path.
	  jdk 'java8'
      maven "maven"
   }
   
   stages
   {
   stage('git clone') {
         steps {
            // Get some code from a GitHub repository
            git 'https://github.com/madhuri1214/madhu.git'
        }  
        }
	stage ('Compile and Build') {
         steps {
           sh '''
           clean install package
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
