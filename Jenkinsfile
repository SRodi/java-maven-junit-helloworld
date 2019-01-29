node {

    notify('Started')
    stage('checkout') {

        git 'https://github.com/SRodi/java-maven-junit-helloworld.git'
    }
    stage('compiling, packaging'){

        sh label: '', script: 'mvn package -DskipTests=true'
    }
    stage('archive'){
        archiveArtifacts 'target/java-maven-junit-helloworld*.jar'
    }
}

def notify(status){
    emailext(
         to: "simone.rodigari@gmail.com",
         subject: "${status}: Job '${env.JOB_NAME}'",
         body: """<p>email body</p>"""
    )

}

//step([$class: 'ArtifactArchiver',
//        Artifacts: "target/java-maven-junit-helloworld*.jar",
//        excludes: null])
//https://github.com/LableOrg/java-maven-junit-helloworld.git