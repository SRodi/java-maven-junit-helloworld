node {

    notify('Started')

    try{
        stage('checkout') {

            git 'https://github.com/SRodi/java-maven-junit-helloworld.git'
        }
        stage('compiling, packaging, testing'){

            sh label: '', script: 'mvn package -DskipTests=false'
        }
        // stash is a temporary archive
        // to ensure same code and dependencies are used throughout the pipeline
        stash name: 'everything',
                excludes: 'test-results/**',
                includes: '**'

        notify('Success')

    } catch (err){
        notify("Error: ${err}")
        currentBuild.result = 'FAILURE'

    }

    stage('archive'){
        // works only on mvn clean verify
        //publishHTML(target: [allowMissing: true,alwaysLinkToLastBuild: false,keepAll: true,reportDir: 'target/site/jacoco',reportFiles: 'index.html',reportName: 'HTML Report',reportTitles: 'Code Coverage'])

        step([$class: 'JUnitResultArchiver',
            //allowEmptyResults: true,
            testResults: 'target/surefire-reports/TEST-*.xml'])

        archiveArtifacts 'target/java-maven-junit-helloworld*.jar'
    }
    notify('Done')
}

node('agent1'){
    sh 'ls'
    sh 'rm -rf *'
    unstash 'everything'
    sh 'ls'
}

node{
    notify("Deploy to staging?")
}

input 'Deploy to staging?'

// stage name: 'Deploy', concurrency: 1

// node{
//     // write build number to index page so we can see this update
//     sh "echo '${env.BUILD_DISPLAY_NAME}' >> log-deploy"

//     // deploy to a docker container mapped to port 3000
//     sh 'docker-compose up -d --build'

//     notify 'Software Deployed!'
// }

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