node('QA Environment') {


    currentBuild.result = "SUCCESS"

    try {

       stage('Checkout'){

          checkout scm
       }

       stage('Test'){

         env.NODE_ENV = "test"

         print "Environment will be : ${env.NODE_ENV}"

         sh 'node -v'
         sh 'npm prune'
         sh 'npm install'
         sh 'npm test'

       }

         stage('Cleanup'){

         echo 'prune and cleanup'
         sh 'npm prune'
         sh 'rm node_modules -rf'

         mail body: 'project build successful',
                     from: 'its.pushkaronline@gmail.com',
                     replyTo: 'its.pushkaronline@gmail.com',
                     subject: 'project build successful',
                     to: 'its.pushkaronline@gmail.com'
       }



    }
    catch (err) {

        currentBuild.result = "FAILURE"

            mail body: "project build error is here: ${env.BUILD_URL}" ,
            from: 'its.pushkaronline@gmail.com',
            replyTo: 'its.pushkaronline@gmail.com',
            subject: 'project build failed',
            to: 'its.pushkaronline@gmail.com'

        throw err
    }

}
