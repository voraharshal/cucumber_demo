node('master') {
    def workSpaceHome = pwd()
    stage('Clean') {
        deleteDir()
    }
    stage('Checkout') {
        checkout scm
    }
    stage('Grunt Process') {
        sh """
            cd ../../QTM_JIRA_Jenkins_Demo/Grunt
            grunt --serverpath="${serverpath}" --apikey="${apikey}" --testRunName="${testRunName}" --platform="${platform}" --labels="${labels}" --components="${components}" --versions="${versions}" --sprint="${sprint}" --comment="${comment}"
        """
    }
    stage('Run') {
       withMaven(jdk: 'JDK', maven: 'maven3', mavenLocalRepo: '', mavenOpts: '', mavenSettingsFilePath: '') {
           sh "mvn test"
       }
    }
}