pipeline {
    agent any

    tools {
        msbuild 'MSBuild'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Anton-osc/Course_W_SP4.git', credentialsId: '', branch: 'master'
            }
        }
        
        stage('Build') {
            steps {
                // Крок для збірки проекту з Visual Studio
                // Встановіть правильні шляхи до рішення/проекту та параметри MSBuild
                bat 'msbuild Sample-Test2.sln /t:Build /p:Configuration=Release'
            }
        }

        stage('Test') {
            steps {
                // Команди для запуску тестів
                bat "x64\\Debug\\Sample-Test2.exe --gtest_output=xml:test_report.xml"
            }
        }
    }

    post {
    always {
        // Publish test results using the junit step
        junit 'test_report.xml'
    }
}
}