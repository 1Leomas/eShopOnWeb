def CLEAN_WORKSPACE = false
def TESTING_FRONTEND = false
pipeline {  
	agent any  
	environment {  
		dotnet = 'C:\\Program Files\\dotnet\\dotnet.exe'  
		ON_SUCCESS_SEND_EMAIL = true
		ON_FAILURE_SEND_EMAIL = true
	}  
	
stages {  

	stage('Clean workspace') {
		when {
			expression { CLEAN_WORKSPACE }
		}
		steps {
			deleteDir()
		}
	}

	stage('Build') {  
		steps {  
			bat 'dotnet build %WORKSPACE%\\eShopOnWeb.sln --configuration Release'
		}  
	}

	stage('Test') {  
		steps { 
			bat 'dotnet test %WORKSPACE%\\tests\\UnitTests\\UnitTests.csproj --logger "junit"'
			junit allowEmptyResults: true, testResults: '**\\TestResults\\**.xml'
		}
	}
	
	stage('Testing frontend') {
		when {
			expression { TESTING_FRONTEND }
		}
		steps {
			echo "TESTING_FRONTEND"
		}
		
	}
	
	stage("Release"){
		steps {
		
			echo "Release"
			
			//bat 'dotnet build  %WORKSPACE%\\jenkins-demo\\HRM\\HRM.sln /p:PublishProfile=" %WORKSPACE%\\jenkins-demo\\HRM\\HRM.API\\Properties\\PublishProfiles\\JenkinsProfile.pubxml" /p:Platform="Any CPU" /p:DeployOnBuild=true /m'
		}
	}
	
	stage('Deploy') {
		steps {
			echo "Deploy"
			
			// Stop IIS
			//bat 'net stop "w3svc"'
			
			// Deploy package to IIS
			//bat '"C:\\Program Files (x86)\\IIS\\Microsoft Web Deploy V3\\msdeploy.exe" -verb:sync -source:package="%WORKSPACE%\\jenkins-demo\\HRM\\HRM.API\\bin\\Debug\\net6.0\\HRM.API.zip" -dest:auto -setParam:"IIS Web Application Name"="HRM.Web" -skip:objectName=filePath,absolutePath=".\\\\PackageTmp\\\\Web.config$" -enableRule:DoNotDelete -allowUntrusted=true'
			
			// Start IIS again
			//bat 'net start "w3svc"'
		}
	}
}} 