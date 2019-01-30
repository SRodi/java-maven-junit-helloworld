node {

    notify('Started')

    try{
        stage('checkout') {

            git 'https://github.com/SRodi/java-maven-junit-helloworld.git'
        }
        stage('compiling, packaging'){

            sh label: '', script: 'mvn package -DskipTests=false'
        }
        stage('archive'){

            step([$class: 'JUnitResultArchiver',
                        //allowEmptyResults: true,
                        testResults: 'target/surefire-reports/TEST-*.xml'])

            archiveArtifacts 'target/java-maven-junit-helloworld*.jar'
        }

        notify('Success')

    } catch (err){
        notify("Error: ${err}")
        currentBuild.result = 'FAILURE'

    }
    notify('Done')
}

def notify(status){
    emailext(
         to: "simone.rodigari@gmail.com",
         subject: "${status}: Job '${env.JOB_NAME}'",
         body: """<p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>"""
    )

}

//step([$class: 'ArtifactArchiver',
//        Artifacts: "target/java-maven-junit-helloworld*.jar",
//        excludes: null])
//https://github.com/LableOrg/java-maven-junit-helloworld.git