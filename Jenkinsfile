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
        
        def reportDir = "${env.WORKSPACE}/reports"
        docker.build('test')
            .inside("-v ${reportDir}:/reports -u root") {
            sh """
                pa11y --reporter json "${SITE_URL}" > /reports/report.json
            """
        }
        step([$class: 'CopyArtifact', filter: 'report.json', fingerprintArtifacts: true, projectName: env.JOB_NAME, selector: [$class: 'StatusBuildSelector', stable: false]])
    }
} 
