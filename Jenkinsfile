pipeline {
	agent{
		label 'tests_node'
	}
	environment{
		adb="/opt/platform-tools/adb"
		ANDROID_HOME="/opt"
		PATH="$PATH:$ANDROID_HOME/tools"
		root="/tmp/android_tests/"
	}
	
	parameters{
		string(defaultValue: "30", description: 'how much time to sleep before the emu starts', name: 'SLEEP_TIME_IN_SECONDS')
	}
	
	stages {
	
		stage("Poll scm..."){
			
			steps{
				
				ws('/tmp/android_tests/'){
					git poll: true, url: 'https://github.com/MirceaM11/android-testing-guide.git' 
				}
			}

		}
		/*
		stage("Preparing the environment..."){
			steps{
				sh'''
					
				'''
			}
		}
		*/
		stage("Build app using gradlew..."){
			steps{
				sh'''
					
					cd /tmp/android_tests/SampleApp
					./gradlew clean assembleDebug 
					./gradlew clean assembleAndroidTest 
				'''
			}
		} 
		stage("Docker emulator start..."){  
			steps{
				sh'''
					
					docker pull tracer0tong/android-emulator:latest
					docker run -d -P tracer0tong/android-emulator:latest
					
				'''
				
			}
		}
		stage("sleep for emulator to come online..."){
				steps{
					
					sleep params.SLEEP_TIME_IN_SECONDS.toInteger()
		}		}
		

		stage("Connect and test..."){
			steps{
				sh'''
					containerID=$(docker ps | awk 'NR == 2 {print $1}')
					echo $containerID
					docker ps
					adbport=$(docker container port $containerID | grep 5555 | awk -F ':' '{print $2}')
					
					$adb connect 0.0.0.0:$adbport
					$adb devices -l
					sleep 40

					containerID=$(docker ps | awk 'NR == 2 {print $1}')
					
					$adb devices -l
					$adb shell input keyevent 82
					$adb install /tmp/android_tests/SampleApp/app/build/outputs/apk/androidTest/debug/app-debug-androidTest.apk
					
					cd /tmp/android_tests/SampleApp
					./gradlew clean test
					./gradlew clean connectedAndroidTest --stacktrace
					docker kill $containerID
				'''
				publishHTML([allowMissing: false, alwaysLinkToLastBuild: true, keepAll: false, reportDir: '/tmp/android_tests/SampleApp/app/build/reports/androidTests/connected', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: ''])
			}
		}
	}
}

