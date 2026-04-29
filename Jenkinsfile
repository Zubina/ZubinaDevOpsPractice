pipeline {
    agent any

    environment {
        APP_NAME = "ZubinaPracticeApp"
        DEV_ENV = "dev"
        QA_ENV  = "qa"
        PROD_ENV = "prod"
    }

 parameters {
        choice(name: 'ENV', choices: ['DEV', 'QA', 'PREPROD','PROD'])
        string(name: 'VERSION', defaultValue: '1.0.0')
    }
    stages {

        stage('Preparation') {
            steps {
                echo 'Preparation Started......'
                sleep 5
                echo 'Preparation Completed......'
            }
        }

        stage('Build') {
            steps {
                echo 'Build Started......'
                build job: 'job1_demo-build-app'
                sleep 5
                echo 'Build Completed......'
            }
        }

        stage('Unit Test') {
            steps {
                echo 'Unit Test Started......'
                build job: 'job2_demo-unit-test'
                sleep 5
                echo 'Unit Test Completed......'
                build job: 'job3_demo-ready-for-testing'
            }
        }
		//stage('Deploy') {//Deploy begin
        //    steps {
        //        echo 'Deployment Started......'
        //        bat "echo Deploying ${params.VERSION} to ${params.ENV}"
        //        sleep 5
        //       echo 'Deployment Completed......'
        //    }
       // }//Deploy end
       
         stage('Parallel Deploy') {
            parallel {
                stage('Deploy DEV') {
                    steps {
                        echo 'Deployment Started......'
                        bat "echo Deploying ${params.VERSION} to DEV"
                        build job: 'job4_demo-smoke-test'
                    }
                }

                stage('Deploy QA') {
                    steps {
                        bat "echo Deploying ${params.VERSION} to QA"
                        build job: 'job4_demo-smoke-test'
                    }
                }

                stage('Deploy PREPROD') {
                    steps {
                        bat "echo Deploying ${params.VERSION} to PREPROD"
                        build job: 'job4_demo-smoke-test'
                    }
                }

                stage('Deploy PROD') {
                    steps {
                        bat "echo Deploying ${params.VERSION} to PROD"
                        echo 'Deployment Completed......'
                    }
                }
                
            }
        }
	}//stages end

    post {
        success {
            echo 'Pipeline Execution Completed......'
           // mail to: 'zubina.mjcet73326@gmail.com',
             //    subject: 'JENKINS PRACTICE-PASS',
             //    body: 'Jenkins Pipeline executed successfully'
        }

        failure {
            echo 'Pipeline Execution Failed......'
            //mail to: 'zubina.mjcet73326@gmail.com',
               //  subject: 'JENKINS PRACTICE-FAIL',
               //  body: 'Jenkins Pipeline failed'
        }
    }
}
