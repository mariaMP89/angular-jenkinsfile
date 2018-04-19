#!groovy

node {
   
   // ------------------------------------
   // -- ETAPA: CHECK TOOLS
   // ------------------------------------
    echo 'Resivsion instalación y versionado de herramientas node y npm'    
    stage('check tools') {
       sh "node -v"
       sh "npm -v"
       
    }
    // ------------------------------------
   // -- ETAPA: Construccion Proyecto angularCLi
   // ------------------------------------
   stage ('Build'){
   
  // -- Configura variables
   echo 'Configurando variables'
 
  // -- Construccion proyecto Angular-CLi
        sh "npm i -g @angular/cli"
        sh "npm rebuild node-sass --force"
   //Descarga SCM
       
  // -- Descarga código desde SCM lqp-ang5
  echo 'Descargando lqp de SCM
   deleteDir()
   checkout scm
   // -- Descarga código desde SCM node-ang5
  // echo 'Descargando estructura de SCM '
   //deleteDir()
   // checkout scm 
 
 '
   }
   // ------------------------------------
   // -- ETAPA: Compilar
   // ------------------------------------
   stage ('Compilar'){
   echo 'Instalacion de NPM'
   withEnv(["NPM_CONFIG_LOGLEVEL=warm"]) {
    sh 'npm install'
        }
   
    echo 'Compilando aplicación'

   // -- Compilando
   echo 'Compilando aplicación'
  milestone()
        sh 'ng build'
  
   }
   // ------------------------------------
   // -- ETAPA: Test
   // ------------------------------------
   stage ('Test'){
   echo 'Ejecutando tests'
        withEnv(["CHROME_BIN=/usr/bin/chromium-browser"]) {
          sh 'ng test --progress=false --watch false'
        }
        junit '**/test-results.xml'
   }
      // ------------------------------------
   // -- ETAPA: Sonar
   // ------------------------------------
   stage ('Sonar'){
   echo 'Ejecutando pruebas Sonar'
   }
   // ------------------------------------
   // -- ETAPA: Empaquetado y versionado
   // ------------------------------------
   stage ('Empaquetar y versionado'){
       // sh 'tar -cvzf dist.tar.gz --strip-components=1 dist'
        //archive 'dist.tar.gz'
   echo 'Instala el paquete generado en el repositorio maven'
   
   }
   // ------------------------------------
   // -- ETAPA: Nexus
   // ------------------------------------
   stage ('Subida Nexus'){
     
    echo 'Subida a Nexus'
      
   }
   
}
