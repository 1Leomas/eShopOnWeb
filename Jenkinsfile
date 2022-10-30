pipeline {  
	agent any  
	environment {  
		dotnet = 'C:\\Program Files\\dotnet\\dotnet.exe'  
		ON_SUCCESS_SEND_EMAIL = "true"
		ON_FAILURE_SEND_EMAIL = "true"
	}
	//triggers {
        //cron('H */2 * * *')
    //}

stages {  
	stage('Build') {  
		steps {  
			bat 'dotnet build %WORKSPACE%\\eShopOnWeb.sln --configuration Release'
		} 
	}

	stage('Testing backend') {
		when {
			expression {
				env.TESTING_BACKEND == "true"
			}
		}
		steps { 
			bat 'dotnet test %WORKSPACE%\\tests\\UnitTests\\UnitTests.csproj --logger "junit"'
			junit allowEmptyResults: true, testResults: '**\\TestResults\\**.xml'
		}
	}
	
	stage('Testing frontend') {
		when {
			expression {
				env.TESTING_FRONTEND == "true"
			}
		}
		steps {
			echo "TESTING_FRONTEND = ${TESTING_FRONTEND}"
		}	
	}

	stage('Clean workspace') {
		when {
			expression {
				env.CLEAN_WORKSPACE == "true"
			}
		}
		steps {
			deleteDir()
		}
	}
}
	post {  
        always {  
             echo 'This will always run'  
        }  
		success {  
			echo 'Build successful' 
			mail 	body: "<b>Build successful</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", 
					charset: 'UTF-8', 
					mimeType: 'text/html', 
					subject: "Successful - Project name: ${env.JOB_NAME}", 
					to: "samuil.rutcovschi@gmail.com"; 
		}  
		failure {  
			echo 'Build failure'  
			mail 	body: "<b>Build failure</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", 
					charset: 'UTF-8', 
					mimeType: 'text/html', 
					subject: "Failure - Project name: ${env.JOB_NAME}", 
					to: "samuil.rutcovschi@gmail.com";  
		}  
    }  
}