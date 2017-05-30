//https://github.com/feedhenry/fh-pipeline-library

fhBuildNode {
    stage('Install Dependencies') {
        dir('fh-messaging') {
            npmInstall {}
        }
        dir('fh-metrics') {
            npmInstall {}
        }
    }

    stage('Build') {
        def buildInfoFileName = 'build-info.json'
        dir('fh-messaging') {
            gruntCmd {
                cmd = 'fh:dist --only-bundle-deps'
            }
            sh "cp output/**/VERSION.txt ."
            def versionTxt = readFile("VERSION.txt").trim()
            buildInfoFileName = writeBuildInfo('fh-messaging', versionTxt)
        }
        dir('fh-metrics') {
            gruntCmd {
                cmd = 'fh:dist --only-bundle-deps'
            }
            sh "cp output/**/VERSION.txt ."
            def versionTxt = readFile("VERSION.txt").trim()
            buildInfoFileName = writeBuildInfo('fh-metrics', versionTxt)
        }
        archiveArtifacts "fh-messaging/dist/fh-messaging*.tar.gz, fh-metrics/dist/fh-metrics*.tar.gz, ${buildInfoFileName}"
    }
}
