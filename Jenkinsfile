pipeline {
    agent any

    stages {
        stage("Checkout code") {
            steps {
                // Checkout code from GitHub and specify the branch
                git branch: 'main', url: 'https://github.com/MEGAROCK666/Jenkins_Selenium_Webdriver_Prectice_Repo_4_8'

            }
        }
        stage("Set up .NET Core") {
            steps {
                bat '''
                echo instaling .NET SDK 6.0
                choco install dotnet-sdk -y --version=6.0.100
                '''
            }
        }
        stage("Restore dependencies") {
            steps {
                // Restore dependencies using the solution file
                bat 'dotnet restore SeleniumBasicExercise.sln'
            }
        }
        stage("Build") {
            steps {
                // Build the project using the solution file
                bat 'dotnet build SeleniumBasicExercise.sln --configuration Release'
            }
        }
        stage("Run tests TestProject1") {
            steps {
                // Run tests using the solution file
                bat 'dotnet test TestProject1/TestProject1.csproj --logger "trx;LogFileName=TestResult.trx"'

            }
        }

        stage("Run tests TestProject2") {
            steps {
                // Run tests using the solution file
                bat 'dotnet test TestProject2/TestProject2.csproj --logger "trx;LogFileName=TestResult.trx"'

            }
        }

        stage("Run tests TestProject3") {
            steps {
                // Run tests using the solution file
                bat 'dotnet test TestProject3/TestProject3.csproj --logger "trx;LogFileName=TestResult.trx"'

            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/TestResults/*.trx', allowEmptyArchive: true
            step ([
                $class: 'MSTestPublisher',
                testResultsFile: '**/TestResults/*.trx'
            ]) 
        }
    }
}