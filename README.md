# devsecops-training-serverless

Set up AWS environment variables

    export AWS_ACCESS_KEY_ID=<your-key-here>
    export AWS_SECRET_ACCESS_KEY=<your-secret-key-here>

Create Serverless Project

    serverless create --template aws-nodejs --path lambda-cicd
    cd lambda-cicd
    npm init

Install CloudGuard Plugin

    npm install -D https://artifactory.app.protego.io/cloudguard-serverless-plugin.tgz

Add the following to the serverless.yml that was created:

    plugins:
     - serverless-cloudguard-plugin

    custom:
      cloudguard:
        fsp:
          Enabled: true
        proact:
          Enabled: true
           
          StoreJobReport: true                         # default is false
    
          Features:
            PermissiveRole:
              Enabled:        true                     # default is true
              FailThreshold:   None                    # default is None
    
            VulnerableDependency:
              Enabled:        true                     # default is true
              FailThreshold:  Critical                 # default is None
    
            CredentialsUsage:
              Enabled:        true                     # default is true
              FailThreshold:  None                     # default is None
    
            RuleViolation:
              Enabled:        true                    # default is true
              FailThreshold:  None                    # default is None

Deploy lambda package

    sls deploy
