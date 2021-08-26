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

    stage('Build de aplicacion') {
      steps {
        echo 'Generando Build'
        timestamps() {
          echo 'Fecha de inicio de build'
        }

        sh 'sh construccion.sh'
      }
    }

    stage('Pruebas unitarias') {
      steps {
        echo 'Ejecutando pruebas unitarias'
        timestamps() {
          echo 'Comienzo de la ejecucion'
        }

        sh 'sh testing_autom.sh'
        mail(subject: 'Pruebas unitarias finalizadas', body: 'Pruebas unitarias finalizadas', from: 'mperezdevops@gmail.com', replyTo: 'mperezdevops@gmail.com', to: 'mperezdevops@gmail.com')
      }
    }

    stage('Testing') {
      parallel {
        stage('Testing') {
          steps {
            echo 'Instalando en servidor de pruebas'
            sh 'sh instalar_testing.sh'
            input 'Las pruebas fueron satisfactorias?'
            mail(subject: 'Software aprobado en testing', body: 'Software aprobado en testing', from: 'mperezdevops@gmail.com', replyTo: 'mperezdevops@gmail.com', to: 'mperezdevops@gmail.com')
          }
        }

        stage('Chrome') {
          steps {
            echo 'Pruebas en google chrome'
          }
        }

        stage('Edge') {
          steps {
            echo 'Pruebas en Edge'
          }
        }

        stage('Firefox') {
          steps {
            echo 'Pruebas en firefox'
          }
        }

      }
    }

  }
}