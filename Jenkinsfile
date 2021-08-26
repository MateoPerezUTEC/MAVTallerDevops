pipeline {
  agent any
  stages {
    stage('Pull request') {
      steps {
        echo 'Aprobacion de pull request'
        mail(subject: 'Hay un pull request pendiente de aprobacion', body: 'Hay un pull request pendiente de aprobacion', from: 'mperezdevops@gmail.com', replyTo: 'mperezdevops@gmail.com', to: 'mperezdevops@gmail.com')
        timestamps() {
          echo 'Fecha/Hora de pull request'
        }

        input 'Aprobar el pull request?'
        git 'https://github.com/MateoPerezUTEC/MAVTallerDevops.git'
      }
    }

  }
}