node("fastlane_Slave"){
    
    stage("Before checkout clean workspace"){
        cleanWs()
    }

    stage("Checkout from git..."){
        checkout scm;
    }

    stage("Build app using fastlane+gradle..."){
        sh'''
            pwd
            echo "Hello! From now we are using fastlane!!"
            echot $PATH
            which fastlane
            fastlane env
            ls -la
            cd SampleApp
        '''
    }
    stage("Tests will be done here..."){
        sh'''
            echo "tests will be run here."
        '''
    }
    
    stage("Delete workspace after work is done..."){
        cleanWs()
    }
}
