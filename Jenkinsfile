stage 'Build'
    node {
        echo 'Building..'
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '8b1b3788-f57f-46fa-8c2d-eba57b1e5afe', url: 'http://10.0.0.238:30080/test-utc/pipeline-testing']]])
    }

stage 'Testing'
    node {
        echo 'Testing..'
        checkout scm
        sh 'make check || true' 
        junit '**/target/*.xml'
    }

stage 'Upload'
    node {
    echo 'Uploading to artifactory..'
    }

stage 'Deploy'
    node {
        echo 'Deploying to server..'
    }
    
