pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                bat '"C:\\Users\\Max\\OneDrive\\Documents\\University\\3Year\\GL\\nuget.exe" restore test_repos.sln'
                bat '"C:\\Program Files (x86)\\MSBuild\\14.0\\Bin\\amd64\\MSBuild.exe" test_repos.sln /t:Build /p:Configuration=Release /p:RestorePackagesConfig=true'
            }
        }
        
        stage('Test') {
            steps {
                bat "x64\\Release\\test_repos.exe --gtest_output=xml:test_report.xml"
            }
        }
    }
    
    post {
        always {
            xunit (tools: [ GoogleTest(pattern: 'test_report.xml') ], skipPublishingChecks: false)
        }
    }
}
