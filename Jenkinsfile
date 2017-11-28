node("fastlane_Slave"){
    
    stage("Before checkout clean workspace."){
        cleanWs()
    }

    stage("Checkout from git."){
        checkout scm;
    }

    stage("Build app using fastlane+gradle."){
        sh'''
            pwd
            echo "Hello! From now we are using fastlane!"
            echo $PATH
            which fastlane
            ls -la
            echo "running beta lane"
            fastlane beta
            echo "beta lane has run correctly, moving on..."
        '''
    }
    stage("Tests will be done here."){
        sh'''
            echo "tests will run here."
        '''
    }
    
    stage("Delete workspace after work is done."){
        cleanWs()
    }
}
