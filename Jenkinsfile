pipeline{
    agent any
    tools{
        jdk 'jdk11'
        maven 'mvn3'
    }

    environment{
        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = '12345678'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vpromvn-central'
        NEXUSIP = '172.31.80.186'
        NEXUSPORT = '8081'
        NEXUS_GRP_REPO = 'vprofile-group'
        NEXUS_LOGIN = 'nexuslogin'
    }

    stages{

        stage('Build'){
            steps{
                sh 'mvn -s settings.xml -DskipTests install'
            }
        }
    }
}
