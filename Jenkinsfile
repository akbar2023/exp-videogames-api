pipeline {
    agent any

    stages {
        stage('Munit Test') {
            steps {
                echo 'Testing..'
                bat 'mvn clean test'
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
                bat 'mvn clean install'
            }
        }
        stage('Deploy') {
          environnement {
        		ANYPOINT_CREDENTIALS = credentials('anypoint.credential')
        	}
            steps {
                echo 'Deploying to cloudHub...'
                bat 'mvn clean deploy -DmuleDeploy -Dmule.version=4.4.0 -Dusername=${ANYPOINT_CREDENTIALS_USR} -Dpassword=${ANYPOINT_CREDENTIALS_PSW} -Denv=Sandbox -Dappname=exp-videogames-api -Dbusiness=cap -DvCore=Micro -Dworkers=1'
                echo 'Deployed...'
            }
        }
    }
}