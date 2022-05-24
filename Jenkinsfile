pipeline {
  agent none
  stages {
    stage("build") {
      agent {
        docker { image 'mcr.microsoft.com/dotnet/sdk:6.0' }
      }

      environment {
          DOTNET_CLI_HOME = "/tmp/DOTNET_CLI_HOME"
          HOME = "/tmp"
      }
      steps {
          sh 'dotnet publish -c Release -r linux-x64 --self-contained true --output build/ NBXplorer/NBXplorer.csproj'
          stash includes: '**/build/', name: 'app'
      }

    }

    /*
    stage("deploy") {
      stages {
        stage("staging") {
          when { branch 'staging' }
          agent { label 'staging' }
          steps {
          }
        }
    
        stage ("production"){
          when { expression {  return env.BRANCH_NAME ==~ /release\/.*/ } }
          agent { label 'production' }
          steps {
            unstash 'app'
            sh 'sudo cp -R build/* /var/blockchains/nbxplorer'
            sh 'sudo chown -R blockchain:blockchain /var/blockchains/nbxplorer'
          }
        }
      }
    }
    */
  }
}


