pipeline {
    agent any
    tools {nodejs "node"}
    stages {
        stage('checkout') {
            steps {
                deleteDir()
                checkout scm
            }
        }
        // install project dependencies
        stage('install') {
            steps {
                sh 'npm install'
            }
        }
        // Basic lint rolling using tslint
        stage('lint') {
            steps {
                sh 'npm run ng lint'
            }
        }
        // unit tests using Karma and Jasmine
        stage('unit') {
            steps {
                sh 'npm run ng test'
            }
        }
        /* end to end tests using protractor
         * Can be run manually but need a version of chrome with a heads up display
        stage('e2e') {
            steps {
                sh 'npm run ng e2e'
            }
        }
        */
        // build the static (ish) pages using angular build function
        stage('build') {
            steps {
                sh 'npm run ng build -- --prod --base-href=.'
            }
        }
        // serve the generated pages to the website's directory (whichever dir is referenced in the webserver config)
        stage('deploy') {
            steps {
                sh '''
                mkdir -p /var/www/html/dpandza/$GIT_BRANCH
                cp -R ./dist/dpandza/* /var/www/html/dpandza/$GIT_BRANCH/
                '''
            }
        }
    }
}
