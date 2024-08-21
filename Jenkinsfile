pipeline {
    agent any
    
    environment {
        VeracodeID = ''
        VeracodeKey    = ''
        VeracodeProfile = 'Jenkins.Java'
        BinaryPath = 'target/verademo.war'
        BranchName = "${env.BRANCH_NAME}"
        // timeStamp = new LocalDate.now()
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
                    sh 'echo "Build Number: ${BUILD_NUMBER}"'
                    sh 'echo "Branch Name: ${BRANCH_NAME}"'
                    sh 'echo "Git Branch: ${GIT_BRANCH}"'
                    sh 'echo "Git local branch: ${GIT_LOCAL_BRANCH}"'
                    sh 'echo "Build ID: ${BUILD_ID}"'
                    // def now = new Date()
                    // def timeStamp =  now.format("yyyy-MM-dd HH:mm:ss", TimeZone.getTimeZone('UTC'))

                    sh 'echo "Date: ${Date}"'


                    sh 'curl -o veracode-wrapper.jar https://repo1.maven.org/maven2/com/veracode/vosp/api/wrappers/vosp-api-wrappers-java/23.4.11.2/vosp-api-wrappers-java-23.4.11.2.jar'
                    sh 'java -jar veracode-wrapper.jar -vid $veracode_id2 -vkey $veracode_key2 -action uploadandscan -appname ${VeracodeProfile} -createprofile true  -version "${GIT_BRANCH} ${BUILD_NUMBER}" -filepath $BinaryPath'
                }
            }
        }
    }
}