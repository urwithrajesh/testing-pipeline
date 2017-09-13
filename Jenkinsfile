stage 'Download'
    node {
        echo 'Building..'
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/urwithrajesh/testing-pipeline']]])
        }

stage 'SonarQube-Testing'
    node {
        echo 'Testing..'
        withSonarQubeEnv('SonarQube') {
          sh ' /var/jenkins_home/tools/hudson.plugins.sonar.SonarRunnerInstallation/office-SonarQube/bin/sonar-scanner -Dsonar.projectBaseDir=/var/jenkins_home/workspace/test-pipeline'
            }
    }

stage 'Junit-Test'
  node {
    echo 'Starting Junit Testing'
  }

stage 'Build'
  node {
    echo 'Building Application'
    nodejs('office-node-') 
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

stage('Deploy approval'){
    input "Deploy to prod?"
}
stage 'Deploy'
    node {
    echo 'Deploying to server..'
    }
