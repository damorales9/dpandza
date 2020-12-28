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

stage('install') {

steps {

sh 'npm install'

}

}

// stage('test') {

// steps {

// sh 'npm run ng test'

// }

// }

stage('build') {

steps {

sh 'npm run ng build -- --prod --base-href=.'

}

}

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
