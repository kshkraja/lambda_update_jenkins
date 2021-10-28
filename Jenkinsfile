pipeline {
	stage('Checkout'){
		checkout scm
		}
	stage('update lambda') {
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'AWS_ACCESS_KEY_ID',
				   AWS_ACCESS_KEY_ID : 'AWS_ACCESS_KEY_ID', AWS_SECRET_ACCESS_KEY : 'AWS_SECRET_ACCESS_KEY']]) {
			dir("files") {
				sh "pwd";
				sh "zip -r lambda_function.zip *";
				sh "chmod 777 *";
				sh "aws lambda update-function-code --function-name welcome --zip-file fileb://lambda_function.zip --region ap-south-1";
				}
			}
		}
}


// steps {
//                 withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'nonprod-supplychain-temp']]) {
//                     script {
//                         sh 'echo  STEP 2 : Update lambda  ====================================='

//                         if (env.BRANCH_NAME == 'development' || env.BRANCH_NAME.startsWith('dev-')) {
// 				prop = readProperties file: 'dev-settings.properties'
// 				echo prop.toString();
// 				dir("supplychain-procurementsrvc-ocdpuller-001/src") {
//                                 sh "pwd";
// 				sh "zip -r lambda_function.zip *";
// 				sh 'chmod 777 *';
// 				sh "aws lambda update-function-code --function-name ${prop.lambdaname} --zip-file fileb://${prop.zipfilename} --region eu-west-1";
//                             }
//                         } else if (env.BRANCH_NAME.startsWith('sit-')) {
//                             prop = readProperties file: 'sit-settings.properties'
// 							echo prop.toString();
//                             dir("supplychain-procurementsrvc-ocdpuller-001/src") {
//                                 sh "pwd";
// 								sh "zip -r lambda_function.zip *";
// 								sh 'chmod 777 *';
// 								sh "aws lambda update-function-code --function-name ${prop.lambdaname} --zip-file fileb://${prop.zipfilename} --region eu-west-1";
//                             }
//                         } else if (env.BRANCH_NAME.startsWith('pre-')) {
//                             prop = readProperties file: 'pre-settings.properties'
// 							echo prop.toString();
//                             dir("supplychain-procurementsrvc-ocdpuller-001/src") {
//                                 sh "pwd";
// 								sh "zip -r lambda_function.zip *";
// 								sh 'chmod 777 *';
// 								sh "aws lambda update-function-code --function-name ${prop.lambdaname} --zip-file fileb://${prop.zipfilename} --region eu-west-1";
//                             }
//                         } else if (env.BRANCH_NAME.startsWith('uat-')) {
//                             prop = readProperties file: 'uat-settings.properties'
// 							echo prop.toString();
//                             dir("supplychain-procurementsrvc-ocdpuller-001/src") {
//                                 sh "pwd";
// 								sh "zip -r lambda_function.zip *";
// 								sh 'chmod 777 *';
// 								sh "aws lambda update-function-code --function-name ${prop.lambdaname} --zip-file fileb://${prop.zipfilename} --region eu-west-1";
//                             }
//                         }
//                     }
//                 }
// pipeline {

//     parameters {
//         string(name: 'environment', defaultValue: 'terraform', description: 'Workspace/environment file to use for deployment')
//         booleanParam(name: 'autoApprove', defaultValue: false, description: 'Automatically run apply after generating plan?')

//     }


//      environment {
//         AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
//         AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
//     }
    
    
    

//    agent  any
//         options {
//                 timestamps ()
//                 ansiColor('xterm')
//             }
//     stages {
//         stage('checkout') {
//             steps {
//                  script{
//                         dir("terraform")
//                         {
//                             git "https://github.com/kshkraja/lambda_jenkin_terraform.git"
//                         }
//                     }
//                 }
//             }

//         stage('Plan') {
//             steps {
//                 sh 'pwd;cd terraform ; terraform init -input=false'
//                 sh 'pwd;cd terraform ; terraform workspace new ${environment}'
//                 sh 'pwd;cd terraform ; terraform workspace select ${environment}'
//                 sh "pwd;cd terraform ; terraform plan -input=false -out tfplan "
//                 sh 'pwd;cd terraform ; terraform show -no-color tfplan > tfplan.txt'
//             }
//         }
//         stage('Approval') {
//            when {
//                not {
//                    equals expected: true, actual: params.autoApprove
//                }
//            }

//            steps {
//                script {
//                     def plan = readFile 'terraform/tfplan.txt'
//                     input message: "Do you want to apply the plan?",
//                     parameters: [text(name: 'Plan', description: 'Please review the plan', defaultValue: plan)]
//                }
//            }
//        }

//         stage('Apply') {
//             steps {
//                 sh "pwd;cd terraform ; terraform apply -input=false tfplan"
//             }
//         }
//     }

//   }
