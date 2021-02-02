# AWS Lambda

## Get Started

Install the serverless library globally in your machine.

```zsh

    npm install -g serverless
```

Then get logged-in in your aws account through your terminal :

```zsh

    serverless config credentials --provider aws --key <key> --secret <secret>  --profile serverless-admin
```

Now create a function :

```zsh

   serverless create --template aws-nodejs --path <path>
```

This will create a folder, containing 3 files : yaml, .gitignore and js file. Insid the .js file, we
will create the javascript function. In your yaml file, add the following fields to your provider
section :

```yaml

    profile: serverless-admin
    region: <region>
```

Now in the .js file, write a simple hello world function :

```js

    module.exports = function helloWorld ( event, context ) {

        console.log('Hello world');

        return 'Hello World';
    }
```

To deploy this function, in the function folder, open a terminal and enter the following command :

```zsh

    serverless deploy -v
```

To execute the deployed lambda function, from our terminal enter the follwoing command :

```zsh

    serverless invoke -f helloWorld -l
```

To update the deployed function, enter the following command :

```zsh

    serverless deploy function -f helloWorld
```

To see all the functions logs, use the following command :

```zsh

    serverless logs -f helloWorld -t
```

-t here means, keep watching the logs and don't exit !

To destroy the function, enter the following command : ( you must stay in the folder, where the function
was created )

```zsh

    serverless remove
```

To mention a particular timeout ( seconds ) and memory size ( mb ), we can edit the yaml file :

```yaml

    timeout: 2
    memory: 512
```

To give IAM configurations, provide the following options in the yaml file : ( for examle if you are
using any additional features, like lambda api or s3 or dynamoDB, then you need permissions for that )

```yaml

    iamRoleStatements:
        - Effect: "Allow"
          Action:
              - "lambda*"
          Resource:
              - "*"
```

To provide environment variables, provide the following configuration in the yaml file :

```yaml

    environment:
        firstName: "John"

    // If we again redefine the env variable in functions section, it will be overrided

    function:
        helloWorld:
            environment:
                firstName: "Marc"
```