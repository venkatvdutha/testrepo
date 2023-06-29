def apps = ['Dataplane', 'Controlplane']

pipeline {
  agent any
  parameters {
    choice(name: 'App', choices: apps, description: 'Select App Name')
   }
  environment {
      JOB_HOME    = "ansible-packer-ami"
  }
  stages {
    stage('Budiling AMI and sharing with PROD account.') {
      steps {
        sh '''#!/bin/bash -e
          cd ${JOB_HOME} || exit
          dp_image="dp"
          cp_image="cp"
          dp_ami_regions="us-west-2","eu-west-1","eu-west-2","ca-central-1","ap-south-1"
          cp_ami_regions="us-west-2","eu-west-1","us-east-1"
          packer validate packer-snapbase-ami-template.json
          echo 
          if [ ${App} == 'Dataplane' ]
          then
             echo "Dataplane"
#             export plane_prefix="dp"
#             packer build -color=false -var="App=${App}" -var="ami_regions1=$dp_ami_regions" packer-snapbase-ami-template.json
          elif [ ${App} == 'Controlplane' ]
          then
             echo "Controlplane"
#             eplane_prefix="cp"
#             packer build -color=false -var="App=${App}" -var="app_image=$cp_image" -var="ami_regions1=$cp_ami_regions" packer-snapbase-ami-template.json
          fi
          '''
        }
    }
  }
  post {
    always {
      cleanWs()
    }
  }
}

