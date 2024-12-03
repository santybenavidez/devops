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
                '''
                import groovy.io.FileType

                    // Only populate if 'Select Specific Files' is chosen
                    if (SELECCION == "Seleccionar contenedor/es") {
                        def list = []
                        def dir = new File("C:\\\\Users\\\\matiash_unitech\\\\Desktop\\\\Nueva carpeta")
                        dir.eachFileRecurse(FileType.FILES) { file ->
                            list << file.name.take(file.name.lastIndexOf('.'))
                        }
                        return list
                    }
                    return [] // Empty list otherwise
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
