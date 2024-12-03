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
                    // Variable SELECCION provista por el usuario
                if (SELECCION == "Seleccionar contenedor/es") {
                    // Ruta al archivo directories.txt (en el workspace)
                    def filePath = "/var/jenkins_home/workspace/directorios-aws/directories.txt"
                    def list = []

                    // Leer el archivo línea por línea si existe
                    def file = new File(filePath)
                    if (file.exists()) {
                        list = file.readLines()
                    } else {
                        println "El archivo directories.txt no existe en el directorio ${filePath}."
                    }

                    // Retornar la lista de subdirectorios
                    return list
                }
                return [] // Retornar lista vacía si no se selecciona opción válida
                '''
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