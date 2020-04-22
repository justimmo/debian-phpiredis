pipeline {
    agent any

    environment {
        NO_INTERACTION = '1'
    }

    stages {
        stage('Build') {
            steps {
                sh label: 'build debian packages', script: 'dpkg-buildpackage --root-command=fakeroot --build=binary --jobs=2 --no-sign'
            }
        }

        stage('Test') {
            steps {
                sh label: 'test 7.2', script: 'make -C build-7.2 test'
                sh label: 'test 7.4', script: 'make -C build-7.4 test'
            }
        }
    }

    post {
        always {
            sh label: 'remove build artifacts', script: 'rm -rf ../phpiredis*.buildinfo ../phpiredis*.changes ../php-phpiredis*.deb'
        }
    }
}
