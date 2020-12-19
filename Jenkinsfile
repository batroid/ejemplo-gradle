pipeline {
    agent any
    parameters { choice(name: 'HERRAMIENTA', choices: ['gradle', 'maven'], description: 'opcion de compilacion')}
    stages {
        stage('Pipeline') {
            steps {
                script {
                //segun el valor del parametro se debe llamar a gradle o maven
                env.TAREA = ''
                echo "HERRAMIENTA SELECCIONADA: ${params.HERRAMIENTA}"   
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"                             
                if (params.HERRAMIENTA == 'gradle'){
                    	def ejecucion = load 'gradle.groovy'
	                    ejecucion.call()
                } else {
                    	def ejecucion = load 'maven.groovy'
	                    ejecucion.call()                    
                }

                }
            }
        }
    }

    post {
        success{
            //: [Nombre Alumno][Nombre Job][buildTool] Ejecución exitosa
            slackSend color: 'good', message: "[Rodrigo Zuniga][${env.JOB_NAME}][${env.HERRAMIENTA}]Ejecucion exitosa"           
        }

        failure{
            //[Nombre Alumno][Nombre Job][buildTool] Ejecución fallida en stage [Stage]
            //la variable env.TAREA esta definida en los groovy
            slackSend color: 'danger', message: "[Rodrigo Zuniga][${env.JOB_NAME}][${env.HERRAMIENTA}]Ejecución fallida en stage [${env.TAREA}]"                   
        }
    }

}
