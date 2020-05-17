pipeline {
   agent any

   stages {
        stage('Copy files changed') {
            steps {
                script {
                    sh "ls"
                    List<String> sourceChanged = sh(
                        returnStdout: true,
                        script: "git diff --name-only HEAD~").split()
                    for (int i = 0; i < sourceChanged.size(); i++) {
                        echo "${sourceChanged[i]}"
                        def dirname = sh(
                            returnStdout: true,
                            script: "dirname ${sourceChanged[i]}"
                        ).trim()
                        echo "dirname: ${dirname}"
                        sh "cp --parents -r ${dirname}/* destination"
                        sh "mv destination/parent-with-changes/* destination"
                    }
                    sh "ls destination"
                }
            }
        }
   }
}
