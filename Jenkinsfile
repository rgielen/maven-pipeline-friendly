node {

    stage('Checkout') {
        checkout scm
    }

    withMaven() {
        stage('Maven Build') {
            sh './mvnw -s settings-ci.xml -P ci clean package'
        }

        stage('Maven Deploy') {
            sh './mvnw -s settings-ci.xml -P ci -DskipTests deploy'
        }
    }

}
