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
            export ANDROID_HOME=/Users/admin/Library/Android/sdk
            echo $ANDROID_HOME
            cd SampleApp
            echo "running alpha lane"
            fastlane alpha
            echo "alpha lane has run correctly, moving on..."
   } 
    stage("Docker emulator and app installation"){    
        sh'''    
            sudo su
            cd /Users/admin/workspace/workspace
            echo "pulling image from git..."
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
