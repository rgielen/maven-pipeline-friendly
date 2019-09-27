node {

    properties([
            parameters([
                    string(name: 'repositoryLocation',
                            defaultValue: 'http://nexus:8081',
                            description: 'The Nexus repository base URL to deploy to',),
                    string(name: 'repositoryCredentialsId',
                            defaultValue: 'nexus-admin',
                            description: 'The Jenkins credentials id for to use for Maven deployment',)
            ])
    ])

    stage('Checkout') {
        checkout scm
    }

    withCredentials([usernamePassword(credentialsId: "$repositoryCredentialsId", usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
        withMaven() {
            stage('Maven Build') {
                sh './mvnw -s settings-ci.xml -Drepo.location=$repositoryLocation -Drepo.username=$USERNAME -Drepo.password=$PASSWORD clean package'
            }

            stage('Maven Deploy') {
                sh './mvnw -s settings-ci.xml -Drepo.location=$repositoryLocation -Drepo.username=$USERNAME -Drepo.password=$PASSWORD -DskipTests deploy'
            }
        }
    }

}
