pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo 'build'
                sh 'pwd'        // /var/lib/jenkins/workspace/demo-for-pipeline_master-I4VIGTM6JE6TBFWUZBZBVPYDJGBTIK2KHOTD5XDPZN2VMFHSUCCQ
                sh 'id'         // uid=112(jenkins) gid=117(jenkins) groups=117(jenkins),118(docker)
                sh 'uname -a'
            }
        }
    }
}
