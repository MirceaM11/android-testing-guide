node("master"){
    
    stage("Before checkout clean workspace."){
        cleanWs()
    }

    stage("Checkout from git."){
        checkout scm;
    }

    stage("Build app using fastlane+gradle."){
        sh'''
            echo "This is the the build..."
       '''
   } 
    stage("Docker emulator and app installation"){    
        sh'''
            echo "Emulator start..."
        '''
    }
    stage("Tests will be done here."){
        sh'''
            echo "tests will run here."
        '''
    }
    /* 
    stage("Delete workspace after work is done."){
        cleanWs()
    }
    */
}
