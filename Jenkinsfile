properties([
    parameters([
    [$class: 'ChoiceParameter',
        name: 'ACCION',
        choiceType: 'PT_RADIO',
        description: 'Seleccionar la acción a realizar',
        script: 
            [$class: 'GroovyScript', script: [classpath: [],
            sandbox: false, script: "return ['Iniciar contenedor/es','Detener contenedor/es','Reiniciar contendedor/es','Recrear contenedor/es']"]
            ]
            ],
    choice(
            name: 'SELECCION',
            choices: ['Todos', 'Seleccionar contenedor/es'],
            description: 'What would you like to do?'
        ), 
    [$class: 'CascadeChoiceParameter', 
        choiceType: 'PT_CHECKBOX', 
        description: 'Seleccionar archivos', 
        filterable: false, 
        name: 'CHOICE', 
        referencedParameters: 'SELECCION', 
        script: [
            $class: 'GroovyScript', 
            fallbackScript: [
                classpath: [], 
                sandbox: false, 
                script: 
                    'return[\'Could not get version\']'
            ], 
            script: [
                classpath: [], 
                sandbox: false,
                script: 
                groovyScript: '''
                import groovy.io.FileType

                // Variable SELECCION provista por el usuario
                if (SELECCION == "Seleccionar contenedor/es") {
                    // Lista dinámica para almacenar los subdirectorios
                    def list = []

                    // Establecer conexión SSH y ejecutar comando remoto
                    def remoteOutput = sh(
                        script: """
                            sshagent (['EC2_SSH_CREDENTIAL_ID']) {
                                ssh -o StrictHostKeyChecking=no ec2-user@ec2-54-227-67-59.compute-1.amazonaws.com\\
                                "find /opt/unitech/composes -mindepth 1 -maxdepth 1 -type d -exec basename {} \\\\;"
                            }
                        """,
                        returnStdout: true
                    ).trim()

                    // Convertir la salida en una lista
                    list = remoteOutput.split('\\n')
                    
                    // Retornar la lista de subdirectorios
                    return list
                }
                return [] // Retornar lista vacía si no se selecciona opción válida
            ''',
            ]
        ]
    ]   
    ]),
    pipelineTriggers([])
])

pipeline {
   agent any  
   stages {

      stage('Printing selected choice') {

         steps {
              script {

                def selectedChoices = params.CHOICE.split(',')
                println "Selected choices: ${selectedChoices}"
                echo params.FILE_SELECTION_TYPE

              }
         }
      }
}
}