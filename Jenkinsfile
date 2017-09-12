stage 'Build'
    node {
        echo 'Building..'
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/urwithrajesh/testing-pipeline']]])
        }

stage 'Testing'
    node {
        echo 'Testing..'
        publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: ''])
        
    }

stage 'Upload'
    node {
    echo 'Uploading to artifactory.........'
    }

stage 'Deploy'
    node {
    echo 'Deploying to server..'
    }
    
