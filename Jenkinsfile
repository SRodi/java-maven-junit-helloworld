node {

    stage('checkout') {

        //https://github.com/LableOrg/java-maven-junit-helloworld.git

        git 'https://github.com/SRodi/java-maven-junit-helloworld.git'

        stage('compiling, packaging'){

            sh label: '', script: 'mvn package -DskipTests=true'

            stage('archive'){
                archiveArtifacts 'target/java-maven-junit-helloworld*.jar'
            }
        }
    }
}

//step([$class: 'ArtifactArchiver',
//        Artifacts: "target/java-maven-junit-helloworld*.jar",
//        excludes: null])