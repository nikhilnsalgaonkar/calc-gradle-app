pipeline {
	agent any
	tools {
	    jdk "JDK17"
	}

	stages {

	    stage('Fetch code') {
            steps {
               git url: 'https://github.com/nikhilnsalgaonkar/calc-gradle-app.git'
            }

	    }


	    stage('Build'){
	        steps{
	           sh 'gradle install -DskipTests'
	        }

	        post {
	           success {
	              echo 'Now Archiving it...'
	              archiveArtifacts artifacts: '**/target/*.war'
	           }
	        }
	    }

	    stage("Sonar Code Analysis") {
        	environment {
                scannerHome = tool 'sonarqube'
            }
            steps {
              withSonarQubeEnv('sonarserver') {
                sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=calc-gradle-app \
                   -Dsonar.projectName=calc-gradle-appe \
                   
              }
            }
        }

        

	}

}