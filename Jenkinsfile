properties([
    parameters([
        string(name: 'SITE_URL', defaultValue: 'https://www.marutisuzuki.com/',
                description: 'URL to test the accesibility against')
    ])
])

SITE_URL = params.SITE_URL ?: 'https://www.marutisuzuki.com//'

stage('Test URL') {
    steps {
            script
                        {
                            sh 'deleteDir()'
                            sh 'checkout scm'
                            sh 'def reportDir = /home/ec2-user/workspace/MARTECH/LQS/test_LQS'
                            docker.build('test')
                            .inside("-v ${reportDir}:/reports") {
                            sh """
                                pa11y --reporter "${SITE_URL}" > /reports/report.json
                            """
                            }
    }
    }
}

