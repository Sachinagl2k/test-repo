properties([
    parameters([
        string(name: 'SITE_URL', defaultValue: 'https://www.marutisuzuki.com/',
    ])
])

SITE_URL = params.SITE_URL ?: 'https://www.marutisuzuki.com//'

stage('Test URL') {
    node {
        deleteDir()
        checkout scm
        
        def reportDir = "${env.WORKSPACE}"
        docker.build('germaniumhq/pa11y')
            .inside("-v ${reportDir}:/") {
            sh """
                pa11y --reporter csv "${SITE_URL}" > report.csv
            """
        }
        step([$class: 'CopyArtifact', filter: 'report.json', fingerprintArtifacts: true, projectName: env.JOB_NAME, selector: [$class: 'StatusBuildSelector', stable: false]])
    }
} 
