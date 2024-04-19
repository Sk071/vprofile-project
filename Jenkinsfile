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
        SONARSERVER = 'sonar-server'
        SONARSCANNER = 'sonar-scanner'
    }

    stages{

        stage('Build'){
            steps{
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post{
                success{
                    echo "Now Archiving..."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('test'){
            steps{
                sh 'mvn test'
            }
        }

        stage('checkstyle Analysis'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }

        stage('Sonar Analysis'){
            environment{
                scannerHome = tool "${SONARSCANNER}"
            }
            steps{
                withSonarQubeEnv("${SONARSERVER}") {
                    sh ''' $({scannerHome}/bin/sonar-scanner)
                    -Dsonar.projectKey=vprofile \
                    -Dsonar.projectName=vprofile \
                    -Dsonar.projectVersion=1.0 \
                    -Dsonar.sources=src/ \
                    -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest \
                    -Dsonar.junit.reportPath=target/surefire-reports \
                    -Dsonar.jococo.reportPath=target/jacoco.exec \
                    -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml '''
            }
        }

    }
}
}
