pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'dotnet build eShopOnWeb.sln'
      }
    }

    stage('Test') {
      parallel {
        stage('Unit') {
          steps {
            sh 'dotnet test tests/UnitTests'
          }
        }

        stage('Integration') {
          steps {
            sh 'dotnet test tests/IntegrationTests'
          }
        }

        stage('Functional') {
          steps {
            sh 'dotnet test tests/FunctionalTests'
          }
        }

      }
    }

    stage('Deployment') {
      steps {
        sh 'dotnet Publish eShopOnWeb.sln -o /var/aspnet'
        catchError(message: 'Functioan problem')
      }
    }

  }
}