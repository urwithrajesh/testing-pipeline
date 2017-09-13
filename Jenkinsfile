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
          sh ' /var/jenkins_home/tools/hudson.plugins.sonar.SonarRunnerInstallation/office-SonarQube/bin/sonar-scanner -Dsonar.projectBaseDir=/var/jenkins_home/workspace/node-build-test'
        //-Dsonar.projectBaseDir=/var/jenkins_home/workspace/node-build-test
        //sonar.projectName=Test Project
}
        //cleanWs()
        //junit testDataPublishers: [[$class: 'AttachmentPublisher']], testResults: '*.xml'
      //  publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: ''])
        sh '''
            npm install
            npm install junit
            export XUNIT_FILE="test/xunit.xml";
            rm -rf test/jshint-result.xml;
    	    rm -rf test/xunit.xml;
           '''
    }

stage 'Upload'
    node {
    echo 'Uploading to artifactory.........'
    }

stage 'Deploy'
    node {
    echo 'Deploying to server..'
    }
