properties([
    parameters([
        string(name: 'SITE_URL', defaultValue: 'https://www.marutisuzuki.com/',
                description: 'URL to test the accesibility against')
    ])
])

SITE_URL = params.SITE_URL ?: 'https://www.marutisuzuki.com//'

stage('Test URL') {
    node {
        deleteDir()
        checkout scm

        docker.build('test')
            .inside {
            sh """
                pa11y -c --reporter json /pa11y.config.json "${SITE_URL}" > report.json
            """
        }
    }
}

