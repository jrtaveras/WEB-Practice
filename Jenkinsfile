pipeline {
    agent any
   
    stages {
        stage('Create web directory')
        {
            input {
              message 'Enter the data'
              parameters {
                    string(name:'AUTHOR', defaultValue: 'Sergio', description: 'Author of the web application deployment ')
                    string(name:'ENVIRONMENT', defaultValue: 'Development',description: 'Environment to deploy')
                 }
            }
            steps{
                echo "The responsible of this project is ${AUTHOR} and and will be deployed in ${ENVIRONMENT}"
                //Fisrt, drop the directory if exists
                bat 'rmdir /s /q \home'
                //Create the directory
                bat 'mkdir \home\jenkin\sweb'
                
            }
        }
        stage('Drop the Apache HTTPD Docker container'){
            steps {
            echo 'droping the container...'
            bat 'docker rm -f apache1'
            }
        }
        stage('Create the Apache httpd container') {
            steps {
            echo 'Creating the container...'
            bat 'docker run -dit --name apache1 -p 9000:80  -v /home/jenkins/web:/usr/local/apache2/htdocs/ httpd'
            }
        }
        stage('Copy the web application to the container directory') {
            steps {
                echo 'Copying web application...'             
                bat 'copy \home\jenkin\sweb\* /home/jenkins/web'
            }
        }
        stage('Checking the app') {
            steps {
                echo 'Testing the web app'
               // bat 'wget http://localhost:9000'
            }
        }       
    }
}
