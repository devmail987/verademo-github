pipeline {
    agent any
    
    environment {
        VeracodeID = ''
        VeracodeKey    = ''
        VeracodeProfile = 'Jenkins.Java'
        CaminhoPacote = 'target/verademo.war'
    }

    stages {
        stage('Git Clone') {
            steps {
                echo 'Pulling...' + env.BRANCH_NAME
                git "https://github.com/devmail987/verademo-github"
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Veracode Upload And Scan') {
            steps {
                sh 'curl -o veracode-wrapper.jar https://repo1.maven.org/maven2/com/veracode/vosp/api/wrappers/vosp-api-wrappers-java/23.4.11.2/vosp-api-wrappers-java-23.4.11.2.jar'
                sh 'java -jar veracode-wrapper.jar -vid ${VeracodeID} -vkey ${VeracodeKey} -action uploadandscan -appname ${VeracodeProfile} -createprofile true  -version $(date +%H%M%s%d%m%y) -filepath ${CaminhoPacote}'
            }
        }
    }
}