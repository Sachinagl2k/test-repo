properties([
    parameters([
        string(name: 'SITE_URL', defaultValue: 'http://germaniumhq.com/',
                description: 'URL to test the accesibility against')
    ])
])

SITE_URL = params.SITE_URL ?: 'https://www.marutisuzuki.com//'

stage('Test URL') {
    node {
        deleteDir()
        checkout scm
        
        def reportDir = "${env.WORKSPACE}"
        docker.build('germaniumhq/pa11y')
            .inside("-v ${reportDir}:/reports") {
            sh """
                pa11y --reporter csv "${SITE_URL}" > reports/report.csv
            """
        }
        step([$class: 'CopyArtifact', filter: 'report.json', fingerprintArtifacts: true, projectName: env.JOB_NAME, selector: [$class: 'StatusBuildSelector', stable: false]])
    }
} 
