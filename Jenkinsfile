pipeline {
    agent {
        label 'agent'
    }

    triggers {
        upstream(upstreamProjects: 'devops-exercise-job-repo', threshold: hudson.model.Result.UNSTABLE)
    }

    stages {
        stage('Retrieve Artifact') {
            steps {
                script {
                    def jobName = 'devops-exercise-job-repo'

                    copyArtifacts(
                        projectName: jobName, 
                        filter: '**/*.jar', 
                        selector: specific('lastSuccessfulBuild')
                    )
                }
            }
        }
        stage('Run Application') {
            steps {
                script {
                    def jarFiles = sh(script: 'find ./target -name "*.jar"', returnStdout: true).trim().split('\n')
                    
                    echo "Found JAR files: ${jarFiles.join(', ')}"
                    
                    def jarFileToRun = jarFiles.find { !it.contains('archive-tmp') }

                    echo "Found JAR file: ${jarFileToRun}"

                    if (jarFileToRun) {
                        sh "java -jar ${jarFileToRun}"
                    } else {
                        error "No suitable JAR file found to run!"
                    }
                    
                }
            }
        }
    }
}
