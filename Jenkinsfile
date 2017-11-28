node("fastlane_Slave"){
    
    
    stage("Checkout from git..."){
        checkout scm;
    }

    stage("Build app using fastlane+gradle..."){
        sh'''
            pwd
            echo "Hello!"
        '''
        fastlane puts "this message is shown using fastlane";

    
    }
}
