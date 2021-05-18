import groovy.json.JsonSlurperClassic

// Global pipiline vars

pipeline {
 
agent any
  stages {
    stage('Checkout') {
        steps{
            echo "Checking out the code from the repo"
            script{
               checkout([$class: 'GitSCM', branches: [[name: "main"]],
               userRemoteConfigs: [[url: githubRepoUrl, credentialsId: githubCredentials]]])
              }
            }
        }
            stage('Get changes') {
                steps{
                    echo "Checking out the code from the repo"
                    script{
                        checkout(scm)
                        def changeLogSets = currentBuild.rawBuild.changeSets     
                        print(changeLogSets)
                        for (int i = 0; i < changeLogSets.size(); i++) {
                            def entries = changeLogSets[i].items
                            for (int j = 0; j < entries.length; j++) {
                                def entry = entries[j]
                                echo "${entry.commitId} by ${entry.author} on ${new Date(entry.timestamp)}: ${entry.msg}"
                                def files = new ArrayList(entry.affectedFiles)
                                for (int k = 0; k < files.size(); k++) {
                                    def file = files[k]
                                    print(file.path)
                                }
                            }
                        }
                    }
                }
            }
        }
    }
