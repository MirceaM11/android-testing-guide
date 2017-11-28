node("fastlane_Slave"){
    
    
    stage("Checkout from git..."){
        checkout scm;
    }

    stage("Build app using fastlane+gradle..."){
        sh'''
            pwd
            echo "Hello! From now we are using fastlane!!"
            mkdir fastlane
            ls -la
        '''
        deleteDir()
    }
}
