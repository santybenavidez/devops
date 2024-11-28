properties([
    parameters([
        [$class: 'ChoiceParameter', 
            choiceType: 'PT_RADIO',
            description: 'Select a cluster',
            filterLength: 1,
            filterable: true,
            multiSelectDelimiter: ',',
            name: 'CLUSTER',
            script: [$class: 'GroovyScript',
                fallbackScript: [
                    classpath: [], 
                    sandbox: true, 
                    script: 'return ["ERROR"]'
                ],
                script: [
                    classpath: [], 
                    sandbox: true, 
                    script: 
       "return['PROD','DEV', 'QA']"
                ]
            ]
        ]
    ])
])

pipeline {
   agent any  
   stages {

      stage('Printing selected choice') {

         steps {
              script {

                println CLUSTER


              }
         }
      }

   }
}
