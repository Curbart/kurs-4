pipeline {
    agent any

    stages {
        stage('Restore Packages') {
    steps {
        bat '.\\nuget.exe restore test_repos.sln'
    }
}  
        stage('Build') {
            steps {   
                bat '"C:/Program Files/Microsoft Visual Studio/18/Community/MSBuild/Current/Bin/MSBuild.exe" test_repos.sln /t:Build /p:Configuration=Debug /p:PlatformToolset=v142 -restore'
            }
        }

        stage('Test') {
            steps {
                bat "x64\\Debug\\test_repos.exe --gtest_output=xml:test_report.xml"
            }
        }
    }

   post {
    always {
        echo 'Publishing Google Test results'
        junit allowEmptyResults: true, testResults: '**/test_report.xml'
    }
}

}