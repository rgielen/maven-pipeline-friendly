node {

    stage('Checkout') {
        checkout scm
    }

    withCredentials([usernamePassword(credentialsId: 'nexus-admin', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
        withMaven() {
            stage('Maven Build') {
                sh './mvnw -s settings-ci.xml -Drepo.username=$USERNAME -Drepo.password=$PASSWORD -P ci clean package'
            }

            stage('Maven Deploy') {
                sh './mvnw -s settings-ci.xml -P ci -Drepo.username=$USERNAME -Drepo.password=$PASSWORD -DskipTests deploy'
            }
        }
    }

}
