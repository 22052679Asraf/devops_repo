
pipeline {
      agent any
      stages {
          stage('ST1 5145881P') {
          steps {
            echo 'Continue from previous phase: Ready to deploy next environment.'
          }
          }
          stage('ST2 5145881P') {
          steps {
            input('Do you want to update to UAT container?')
          }
          }
          stage('ST3 5145881P') {
          when {
                not {
                    branch "UAT container NOT updated"
                }
          }
          steps {
                 sh '''#!/bin/bash
                 puppet resource file /tmp/clone ensure=absent force=true;
                 puppet resource file /tmp/clone ensure=directory;
	   cd /tmp/clone;
	   git clone https://github.com/22052679Asraf/devops_repo.git;
                 targets=testsvr5145881p;
                 locate_script='/tmp/clone/devops_repo/script_to_run';
                 bolt script run $locate_script -t $targets -u clientadm -p user123 --no-host-key-check --run-as root;
                 '''
                 echo "UAT container updated"
          }
          }
          stage('ST4 5145881P') {
          steps {
            input('Do you want to deploy to Production container?')
                
          }
          }
          stage('ST5 5145881P') {
          when {
                not {
                    branch "Production container NOT updated"
                }
          }
          steps {
                 sh '''#!/bin/bash
                 targets=prodsvr5145881p;
                 locate_script='/tmp/clone/devops_repo/script_to_run';
                 bolt script run $locate_script -t $targets -u clientadm -p user123 --no-host-key-check --run-as root;
                 '''
                 echo "Production container updated"
          }
          }
          stage('ST6 5145881P') {
          steps {
            echo 'Completed updating to Production Container'
          }
          }
      }
}
