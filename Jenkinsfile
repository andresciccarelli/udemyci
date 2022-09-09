pipeline {
    agent any
    
    environment {
        def DATETIME = sh(script: "echo `date '+%Y%m%d-%H%M%S'`", returnStdout: true).trim()
    }
        stages{
        stage("Env Variables"){
            steps{
                bat "set"                                                     
            }
        }
    }
    /*

    stages {
        stage('Starting') {
            steps {
                echo '========================================================================================================================================================\n========================================================================================================================================================'
                echo 'Starting DeployMarketUI'
                echo 'Sending Message to Slack'
                //wrap([$class: 'BuildUser']) {
                slackSend color: "good", message: "Build Market UI starting...\n Branch/Tag:${sha1}\n Repository: Market \nTriggered by: " 
               // }
            }
        }*/
       /* stage ('Checkout-Repository') {
            steps {
                echo '========================================================================================================================================================\n========================================================================================================================================================'
                echo 'Checking out repository...'
                withCredentials([string(credentialsId: 'github-cred-token', variable: 'Token')]) {
					powershell('Get-ChildItem ./ -Recurse -Force | Remove-Item -Force -Confirm:$false -Recurse')
                    powershell('git clone -b $($env:branch) https://' + Token + '@github.com/southxchange/market.git .');
                }
            }
        }*/
        /*stage ('Build-Payment-Widget')
        {
            steps {
                echo '========================================================================================================================================================\n========================================================================================================================================================'
                echo 'Building Payment widget...'
                powershell('npm ci --prefix ./Market.Web.PaymentWidget');
                powershell('npm run build:$($env:Target) --prefix ./Market.Web.PaymentWidget');
            }
        }
        stage ('Build-Solution')
        {
            steps {
                echo '========================================================================================================================================================\n========================================================================================================================================================'
                echo 'Building solution...'
                powershell('./buildMarketUI.ps1 $($env:Configuration); exit $lastexitcode')
            }
        }/*
        /*stage ('Stop-Web-App') {
            steps {
				echo '========================================================================================================================================================\n========================================================================================================================================================'
                echo 'Stopping Azure Web App.'
                withCredentials([usernamePassword(credentialsId: 'azure-admin-backend-creds', passwordVariable: 'pass', usernameVariable: 'user')]) {
                    powershell('az login --service-principal -u ' + user + ' -p ' + pass + ' --tenant a377b6ba-b640-4aaa-97b2-a81fb186a635');
                    powershell('az webapp stop --name $($env:WebAppName) --resource-group $($env:ResourceGroup)');
                }
            }
        }
        stage ('Publish')
        {
            steps {
                echo '========================================================================================================================================================\n========================================================================================================================================================'
                echo 'Publish Azure Web App.'
				powershell('az webapp deployment source config-zip --name $($env:WebAppName) --resource-group $($env:ResourceGroup) --src ./Market.Web/artifacts/MarketUI$($env:Configuration).zip');
            }
        }
        stage ('Start-Web-App') {
            steps {
				echo '========================================================================================================================================================\n========================================================================================================================================================'
                echo 'Starting Azure Web App.'
                powershell('az webapp start --name $($env:WebAppName) --resource-group $($env:ResourceGroup)');
            }
        }*/
    }
    post {
    success {
      slackSend channel: '#builds', color: 'good', message: "Build Market UI Successfully"
      //powershell('Get-ChildItem ./ -Recurse -Force | Remove-Item -Force -Confirm:$false -Recurse')
    }
    failure {
      slackSend channel: '#builds', color: 'danger', message: "@here Build Market UI Failed\nSee the logs http://${params.Target}.jenkins.southxchange.com:8748/job/Deploys/job/${params.Target}/job/DeployMarketUI/${currentBuild.number}/consoleFull"
    }
  }
}
