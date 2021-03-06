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

    stage('Instalacion preproduccion') {
      steps {
        echo 'Instalando en ambiente de preproduccion'
        sh 'sh instalar_prep.sh'
        timestamps() {
          echo 'Instalado en preproduccion'
        }

        mail(subject: 'Instalacion en preproduccion finalizada', body: 'Instalacion en preproduccion finalizada', from: 'mperezdevops@gmail.com', replyTo: 'mperezdevops@gmail.com', to: 'mperezdevops@gmail.com')
      }
    }

    stage('Aprobacion cliente') {
      steps {
        echo 'Sistema listo para ser aprobado por el cliente'
        mail(subject: 'Hay una nueva version para aprobar', body: 'Hay una nueva version para aprobar', from: 'mperezdevops@gmail.com', replyTo: 'mperezdevops@gmail.com', to: 'mperezdevops@gmail.com')
        input 'Aprobar software?'
        mail(subject: 'Software Aprobado', body: 'Software Aprobado', from: 'mperezdevops@gmail.com', replyTo: 'mperezdevops@gmail.com', to: 'mperezdevops@gmail.com')
      }
    }

    stage('Publicacion en produccion') {
      steps {
        echo 'Instalando en produccion'
        sh 'sh instalar_prod.sh'
        mail(subject: 'El software quedo desplegado en produccion', body: 'El software quedo desplegado en produccion', from: 'mperezdevops@gmail.com', replyTo: 'mperezdevops@gmail.com', to: 'mperezdevops@gmail.com')
        timestamps() {
          echo 'Fecha de publicacion'
        }

      }
    }

  }
}