node("master"){

    stage("Poll scm..."){
        
        ws('/tmp/android_tests/'){
            git poll: true, url: 'https://github.com/MirceaM11/android-testing-guide.git' 
        }

    }
    stage("Preparing the environment..."){
        sh'''
            export ANDROID_HOME=/opt
            export PATH=$PATH:$ANDROID_HOME/tools
            sudo chmod -R 777 /tmp/android_test/
        '''
    }
    stage("Build app using gradlew..."){
        sh'''
            cd /tmp/android_tests/SampleApp
            ./gradlew assembleDebug --stacktrace 
            ./gradlew assembleDebugTest --stacktrace
       '''
    } 
    stage("Docker emulator and app installation"){    
        sh'''
            echo "Emulator start..."
        '''
    }
    stage("Tests will be done here..."){
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
