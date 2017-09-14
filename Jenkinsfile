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

//slackSend baseUrl: 'https://utdigital.slack.com/services/hooks/jenkins-ci/', channel: 'chatops', message: 'Build Started: ${env.JOB_NAME} ${env.BUILD_NUMBER}', teamDomain: 'utdigital', token: 'a8p3yJ8BdYURLzmorsUyaIaI'
def summary = "Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' "
slackSend baseUrl: 'https://utdigital.slack.com/services/hooks/jenkins-ci/', channel: 'chatops', summary , teamDomain: 'utdigital', token: 'a8p3yJ8BdYURLzmorsUyaIaI'
