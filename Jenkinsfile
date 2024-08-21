pipeline {
    agent any
    
    environment {
        VeracodeID = ''
        VeracodeKey    = ''
        VeracodeProfile = 'Jenkins.Java'
        BinaryPath = 'target/verademo.war'
        BranchName = "${env.BRANCH_NAME}"
    }

    stages {
        stage('Git Clone') {
            steps {
                echo 'Pulling...' + env.BRANCH_NAME
                git branch: 'main', url: 'https://github.com/devmail987/verademo-github'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Veracode Upload And Scan') {
            steps {
                // withCredentials([usernamePassword(credentialsId: 'TestCredentials', passwordVariable: 'vkey', usernameVariable: 'vid')]) {
                //     sh 'curl -o veracode-wrapper.jar https://repo1.maven.org/maven2/com/veracode/vosp/api/wrappers/vosp-api-wrappers-java/23.4.11.2/vosp-api-wrappers-java-23.4.11.2.jar'
                //     sh 'java -jar veracode-wrapper.jar -vid ${vid} -vkey ${vkey} -action uploadandscan -appname ${VeracodeProfile} -createprofile true  -version $(date +%H%M%s%d%m%y) -filepath ${CaminhoPacote}'
                // }

                // withCredentials([usernamePassword(credentialsId: 'VeracodeCredentials', passwordVariable: '$veracode_key', usernameVariable: '$veracode_id')]) {
                //     sh 'curl -o veracode-wrapper.jar https://repo1.maven.org/maven2/com/veracode/vosp/api/wrappers/vosp-api-wrappers-java/23.4.11.2/vosp-api-wrappers-java-23.4.11.2.jar'
                //     sh 'java -jar veracode-wrapper.jar -vid $veracode_id -vkey $veracode_key -action uploadandscan -appname ${VeracodeProfile} -createprofile true  -version $(date +%H%M%s%d%m%y) -filepath ${CaminhoPacote}'
                // }

                withCredentials([usernamePassword(credentialsId: 'VeracodeCredentials2', passwordVariable: 'veracode_key2', usernameVariable: 'veracode_id2')]) {
                    sh 'pwd'
                    sh 'ls target'
                    sh 'curl -o veracode-wrapper.jar https://repo1.maven.org/maven2/com/veracode/vosp/api/wrappers/vosp-api-wrappers-java/23.4.11.2/vosp-api-wrappers-java-23.4.11.2.jar'
                    sh 'java -jar veracode-wrapper.jar -vid $veracode_id2 -vkey $veracode_key2 -action uploadandscan -appname ${VeracodeProfile} -createprofile true  -version "$env.BRANCH_NAME" -filepath $BinaryPath'
                }
            }
        }
    }
}