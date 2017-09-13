stage 'Build'
    node {
        echo 'Building..'
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/urwithrajesh/testing-pipeline']]])
        
      //  nodejs('office-node-') {
    //    sh '''npm install
      // '''
       // }
        }

stage 'Testing'
    node {
        echo 'Testing..'
        withSonarQubeEnv('SonarQube') {
            sonar.projectName=Test Project
    // some block.  
}
        //cleanWs()
        //junit testDataPublishers: [[$class: 'AttachmentPublisher']], testResults: '*.xml'
      //  publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: ''])
        
    }

stage 'Upload'
    node {
    echo 'Uploading to artifactory.........'
    }

stage 'Deploy'
    node {
    echo 'Deploying to server..'
    }
