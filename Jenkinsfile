// SCRIPTED
//node {
//	echo "Build"
//	echo "Test"
//	echo "Integration Test"
//}

// DECLARATIVE
pipeline {
	agent any
	//agent { docker {image 'maven:3.6.3'} }
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages { 
		stage('Checkout') {
			steps {
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"	

			}
		}
		stage('Compile') {
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
				sh "mvn test"
				//echo "Test"

			}
		}
		stage('Integration Test') {
			steps {
				//echo "Integration Test"
				sh "mvn failsafe:integration-test failsafe:verify"

			}
		}
	} 
	post {
		always {
			echo 'Im awesome. I run always'
		}
		success {
			echo 'I run when you are sucessful'
		}
		failure {
			echo 'I run when you fail'
		}
		
	}
}
