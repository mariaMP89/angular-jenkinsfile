#!groovy

node {
   

// ---------------------------------------------------------------------------
// -- ETAPA: Construccion Proyecto angularCLi
// ---------------------------------------------------------------------------
    
    stage ('Build'){
   
      
     // -- Descarga código desde SCM liberneo-app-ang5
  
        echo 'Descargando SCM'
        //deleteDir()
        "cmd /cnpm checkout scm".execute() 
        "checkout scm" .execute()
    }

// ---------------------------------------------------------------------------
// -- ETAPA: Compilar
// ---------------------------------------------------------------------------
  
   stage ('Compilar'){
  
    // -- Ejecucion del npm install para la obtencion del node_module
        
        echo 'Instalacion de NPM'
       "cmd /cnpm install".execute()  
      "npm install" .execute()
        
    // -- Compilando
  
        echo 'Compilando aplicación'
        milestone()

    // --  MILESTONE  garantiza que una compilación más antigua no anule una compilación más nueva,
    // por lo que nunca se permitirá que la compilación más antigua pase un milestone
    // (se cancela) si una compilación más nueva ya pasó
   "cmd /c ng build".execute()

   "ng build".execute()

      
    }

// ---------------------------------------------------------------------------
// -- ETAPA: Test
// ---------------------------------------------------------------------------
   
    stage ('Test'){
   
    // -- Ejecucion de los test unitarios 

        echo 'Ejecutando tests'
        withEnv(["CHROME_BIN=/usr/bin/chromium-browser"]) {
            sh 'ng test --progress=false --watch false'
        }
        junit '**/test-results.xml'
    }

// ---------------------------------------------------------------------------
// -- ETAPA: Sonar
// ---------------------------------------------------------------------------

    stage ('Sonar'){

    // -- Ejecucion de las pruebas en SonarQube
        echo 'Ejecutando pruebas Sonar'

   }

// ---------------------------------------------------------------------------
// -- ETAPA: Empaquetado y versionado
// ---------------------------------------------------------------------------

    stage ('Empaquetar y versionado'){

    // -- Empaquetado del proyecto
        echo 'Empaquetado del Proyecto'
        // sh 'tar -cvzf dist.tar.gz --strip-components=1 dist'
        //archive 'dist.tar.gz'
    // -- Versionado del proyecto      
        echo 'Versionado del proyecto'   
   }

// ---------------------------------------------------------------------------
// -- ETAPA: Nexus
// ---------------------------------------------------------------------------
    
    stage ('Subida Nexus'){

    // -- Subida a NExus del proyecto empaquetado 
        echo 'Subida a Nexus'  
   }
 
 // --  Para publicar npm Snapshot 
 //stage('Publish NPM snapshot') {
      //def currentVersion = sh(returnStdout: true, script: "npm version | grep \"{\" | tr -s ':'  | cut -d \"'\" -f 4").trim()
     // def newVersion = "${currentVersion}-${buildNumber}"
      //sh "npm version ${newVersion} --no-git-tag-version && npm publish --tag next"
   // }


}
