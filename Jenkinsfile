pipeline{
    agent any
    tools{
        jdk 'jdk11'
        maven 'mvn3'
    }

    environment{
        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin123'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vpromvn-central'
        NEXUS_IP = '18.206.145.4'
        NEXUS_PORT = '8081'
        NEXUS_GRP_REPO = 'vprofile-group'
        NEXUS_LOGIN = 'nexuslogin'
    }

    stages{

        stage('Build'){
            steps{
                sh 'mvn -s settings.xml'
            }
        }
    }
}
