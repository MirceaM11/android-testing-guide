node("master"){

    stage("Poll scm..."){
        
        ws('/tmp/android_tests/'){
            git poll: true, url: 'https://github.com/MirceaM11/android-testing-guide.git' 
        }

    }
    stage("Preparing the environment..."){
        sh'''
            
        '''
    }
    stage("Build app using gradlew..."){
        sh'''
            export ANDROID_HOME=/opt
            export PATH=$PATH:$ANDROID_HOME/tools
            cd /tmp/android_tests/SampleApp
            ./gradlew assembleDebug --stacktrace 
            ./gradlew assembleAndroidTest --stacktrace
       '''
    } 
    stage("Docker emulator and app installation"){    
        sh'''
			export adb=/opt/platform-tools/adb
			echo $adb
			docker pull tracer0tong/android-emulator:latest
			docker run -d -P tracer0tong/android-emulator:latest
			containerID=$(docker ps | awk 'NR == 2 {print $1}')
			echo $containerID
			docker ps
			adbport=$(docker container port $containerID | grep 5555 | awk -F ':' '{print $2}')
            $adb connect 0.0.0.0:$adbport
        '''
    }
    stage("Tests will be done here..."){
        sh'''
			export ANDROID_HOME=/opt
            export PATH=$PATH:$ANDROID_HOME/tools
			cd /tmp/android_tests/SampleApp
			./gradlew test
			./gradlew connectedAndroidTest --stacktrace
			containerID=$(docker ps | awk 'NR == 2 {print $1}')
			docker kill $containerID
        '''
		publishHTML([allowMissing: false, alwaysLinkToLastBuild: true, keepAll: false, reportDir: '/tmp/android_tests/SampleApp/app/build/reports/androidTests/connected', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: ''])
    }
	
    /* 
    stage("Delete workspace after work is done."){
        cleanWs()
    }
    */
}
