# devsecops-training-serverless

Set up AWS cli

    awscli config

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
