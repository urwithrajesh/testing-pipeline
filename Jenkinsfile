stage 'Download'
    node {
        echo 'Building..'
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/urwithrajesh/testing-pipeline']]])
        }

stage 'SonarQube'
    node {
        echo 'Testing...'
        withSonarQubeEnv('SonarQube') {
          sh ' /var/lib/jenkins/tools/hudson.plugins.sonar.SonarRunnerInstallation/SonarQube/bin/sonar-scanner -Dsonar.projectBaseDir=/var/lib/jenkins/workspace/CICD-Demo'
            }
    }

stage 'Junit'
  node {
    echo 'Starting Junit Testing'
  }

stage 'Build'
  node {
    echo 'Building Application'
    nodejs('NodeJS') 
      {
        sh '''
          npm install
          npm install junit
          npm start &
        '''
  }
}
stage 'Upload'
    node {
    echo 'Uploading to artifactory.........'
    }

stage('Approval'){
    input "Deploy to prod?"
}
stage 'Deploy'
    node {
    echo 'Deploying to server..'
    }

// SLACK Settings ########


def notifyBuildSlack(String buildStatus, String toChannel) {
  // build status of null means successful
  buildStatus =  buildStatus ?: 'SUCCESSFUL'
  def toChannel = "#chatops"
  def summary = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (<${env.BUILD_URL}|Jenkins>)"

  // Default values
  def colorCode = '#FF0000'

  if (buildStatus == 'STARTED' || buildStatus == 'UNSTABLE') {
    colorCode = '#FFFF00' // YELLOW
  } else if (buildStatus == 'SUCCESSFUL') {
    colorCode = '#00FF00' // GREEN
  } else {
    colorCode = '#FF0000' // RED
  }

  // Send slack notifications all messages
  slackSend (color: colorCode, message: summary, channel: toChannel)
}


def notifyDeploySlack(String buildStatus, String toChannel) {
  // build status of null means successful
  buildStatus =  buildStatus ?: 'SUCCESSFUL'

  def summary = "${buildStatus}: Deploy '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (<${env.BUILD_URL}|Jenkins>)"

  def colorCode = '#FF0000'

  if (buildStatus == 'STARTED' || buildStatus == 'UNSTABLE') {
    colorCode = '#FFFF00' // YELLOW
  } else if (buildStatus == 'SUCCESSFUL') {
    colorCode = '#008000' // GREEN
  } else {
    colorCode = '#FF0000' // RED
  }

  // Send slack notifications all messages
  slackSend (color: colorCode, message: summary, channel: toChannel)
}


//slackSend baseUrl: 'https://utdigital.slack.com/services/hooks/jenkins-ci/', channel: 'chatops', message: 'Build Started: ${env.JOB_NAME} ${env.BUILD_NUMBER}', teamDomain: 'utdigital', token: 'a8p3yJ8BdYURLzmorsUyaIaI'
