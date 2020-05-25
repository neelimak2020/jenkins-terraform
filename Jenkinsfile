// Jenkinsfile

try {
  stage('checkout') {
    node {
ws('C:\\Users\\Neelima\\Desktop\\t2') {
    
      checkout scm
		}
    }
  }
	stage('terraform started') {
		node{
bat label: '', script: '''echo starting pipeline'''     
		}
        }

  // checking terraform version
  stage('version') {
    node {
   	    bat label: '', script: 'terraform --version'    

    }
  }


  // Run terraform init
	stage('init') {
    node {
	    ws('C:\\Users\\Neelima\\Desktop\\t1') {

    withCredentials([[
		$class: 'AmazonWebServicesCredentialsBinding',
		 accessKeyVariable: 'AWS_ACCESS_KEY_ID',
		 credentialsId: 'd663c70e-cff8-4c07-b5a6-fcffceffafe9',
		 secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
      ]]) {
        ansiColor('xterm') {
bat label: '', script: 'terraform init'      
	}
      }
    }
  }
  }

  
  // Run terraform plan
  stage('plan') {
    node {
	    ws('C:\\Users\\Neelima\\Desktop\\t1') {

      withCredentials([[
      $class: 'AmazonWebServicesCredentialsBinding',
                 accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                 credentialsId: 'd663c70e-cff8-4c07-b5a6-fcffceffafe9',
                 secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
     ]]) {
        ansiColor('xterm') {
bat label: '', script: 'terraform plan'      
        }
      }
    }
  }
  }
  if (env.BRANCH_NAME == 'master') {

    // Run terraform apply
    stage('apply') {
      node {
	      ws('C:\\Users\\Neelima\\Desktop\\t1') {

        withCredentials([[
		 $class: 'AmazonWebServicesCredentialsBinding',
                 accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                 credentialsId: 'd663c70e-cff8-4c07-b5a6-fcffceffafe9',
                 secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
       ]]) {
          ansiColor('xterm') {
		  bat label: '', script: 'terraform apply -auto-approve'     

          }
        }
      }
    }
    }
    // Run terraform show
    stage('show') {
      node {
	      ws('C:\\Users\\Neelima\\Desktop\\t1') {

        withCredentials([[
	 $class: 'AmazonWebServicesCredentialsBinding',
                 accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                 credentialsId: 'd663c70e-cff8-4c07-b5a6-fcffceffafe9',
                 secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
        ]]) {
          ansiColor('xterm') {
		bat label: '', script: 'terraform show'     

	  }  
          }
        }
      }
    }
  }
  currentBuild.result = 'SUCCESS'
}
catch (org.jenkinsci.plugins.workflow.steps.FlowInterruptedException flowError) {
  currentBuild.result = 'ABORTED'
}
catch (err) {
  currentBuild.result = 'FAILURE'
  throw err
}
finally {
  if (currentBuild.result == 'SUCCESS') {
    currentBuild.result = 'SUCCESS'
}
}
