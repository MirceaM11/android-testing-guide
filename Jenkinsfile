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
        '''
   } 
    stage("Docker emulator and app installation"){    
        sh'''    
            
            cd /Users/admin/workspace/workspace
            echo "pull docker image..."
            sudo /usr/local/bin/docker pull tracer0tong/android-emulator:latest
            sudo /usr/local/bin/docker images
            sudo /usr/local/bin/docker run -d -P tracer0tong/android-emulator:latest
            pwd 
            cd /Users/admin/workspace/workspace
            touch containerIDfile
            sudo /usr/local/bin/docker ps >> containerIDfile
            containerID=$( awk 'NR == 2 {print $1}' containerIDfile )
            echo $containerID
            sudo /Users/admin/Library/Android/sdk/platform-tools/adb devices -l
            
            sudo /usr/local/bin/docker kill $containerID
    

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
