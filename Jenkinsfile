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
            containerID=$(sudo /usr/local/bin/docker ps | awk 'NR == 2 {print $1}')
            echo $containerID
            adbport=$(sudo /usr/local/bin/docker container port $containerID | grep 5555 | awk -F ':' '{print $2}')
            sudo /usr/local/bin/docker ps
            sudo /Users/admin/Library/Android/sdk/platform-tools/adb -s connect 0.0.0.0:$adbport
            sudo /Users/admin/Library/Android/sdk/platform-tools/adb devices -l
            sudo /Users/admin/Library/Android/sdk/platform-tools/adb -s 0.0.0.0:$adbport install /Users/admin/workspace/workspace/android_fastPipe/SampleApp/app/build/outputs/apk/debug/app-debug.apk   
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
