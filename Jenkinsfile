pipeline {
    agent any
    parameters {
        booleanParam(name: 'RUN_EXTRA_CHECK', defaultValue: true, description: 'Run the extra check stage?')
    }
    stages {
        stage('Checkout') {
            steps {
                git gitbranch: 'main', url: 'https://github.com/student-aniketroczz/Jenkins-conditional-execution.git'
            }
        }
        stage('Build') {
            steps {
                bat 'python -m py_compile app.py'
                echo 'Build successful: app.py compiled with no syntax errors'
            }
        }
        stage('Extra Check') {
            when {
                expression { params.RUN_EXTRA_CHECK == true }
            }
            steps {
                echo 'Running extra check: verifying greet() output format...'
                bat 'python -c "from app import greet; print(greet(\'Student\'))"'
            }
        }
    }
}
