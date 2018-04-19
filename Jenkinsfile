#!groovy

node {
   
// ---------------------------------------------------------------------------
// -- ETAPA: CHECK TOOLS
// ---------------------------------------------------------------------------
      
    stage('check tools') {
     
        echo 'Resivsion instalación y versionado de herramientas node y npm'

    // -- Se comprueba si esta instalada la version igual o superor a 8 del node
        sh 'apt-get update'
        echo 'Version instalada del nodejs'
        def nodeV =  sh "node -v"
        if (nodeV < 8 || nodeV == null){
           sh 'apt-get install nodejs'
        }else{
            sh "node -v"
        }

    // -- Se comprueba si esta instalada la version del npm
        
        echo 'Version instalada de npm'
        def npmV = sh "npm -v"
        if(npm == null){
            sh "install npm"
        }else{
            sh "npm -v"
        }
    }

// ---------------------------------------------------------------------------
// -- ETAPA: Construccion Proyecto angularCLi
// ---------------------------------------------------------------------------
    
    stage ('Build'){
   
     // -- Construccion proyecto Angular-CLi

        sh "npm i -g @angular/cli"
        // sh "npm rebuild node-sass --force"
       
     // -- Descarga código desde SCM liberneo-app-ang5
  
        echo 'Descargando lqp + lqde SCM'
        deleteDir()
        checkout scm

    // -- Descarga código desde SCM lqp-ang5
  
        echo 'Descargando lqp SCM'
        sh "cd node_ang5/src/app"
        checkout scm

    // -- Descarga código desde SCM lqpBridge
  
        echo 'Descargando  lqpBridge SCM'
        sh "cd node_ang5/src/app"
        checkout scm
    }

// ---------------------------------------------------------------------------
// -- ETAPA: Compilar
// ---------------------------------------------------------------------------
  
   stage ('Compilar'){
  
    // -- Ejecucion del npm install para la obtencion del node_module
        
        echo 'Instalacion de NPM'
        sh 'npm install'
        
    // -- Compilando
  
        echo 'Compilando aplicación'
        milestone()

    // --  MILESTONE  garantiza que una compilación más antigua no anule una compilación más nueva,
    // por lo que nunca se permitirá que la compilación más antigua pase un milestone
    // (se cancela) si una compilación más nueva ya pasó

        sh 'ng build'
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

