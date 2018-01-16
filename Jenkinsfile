node("master"){

    stage("Checkout from git..."){
        git poll: true, url: 'https://github.com/MirceaM11/android-testing-guide.git' 
        //git branch: 'testbranch1', url: 'https://github.com/MirceaM11/android-testing-guide.git';
        
    }

    stage("Build app using gradle..."){
        sh'''
            echo "This is the the build..."
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
