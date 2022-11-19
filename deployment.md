This project can only be deployed with the 2021 beta version of the SAM cli (`sam-beta-cdk`). To install this version do:
```
$ wget https://github.com/aws/aws-sam-cli/releases/download/sam-cli-beta-cdk/aws-sam-cli-linux-x86_64.zip
$ unzip aws-sam-cli-linux-x86_64.zip -d sam-installation
$ [sudo] ./sam-beta-installation/install
$ sam-beta-cdk --version
SAM CLI, version 1.29.0.dev202108311500
```

Once installed, run:
```
$ npm install
$ npm run build
$ npm run deploy
```

Example CDK deploy log:
```
CdkDayStack: deploying...
[0%] start: Publishing 86bb9646ec2db1228e0311c14da31648235c91b989b962349fa001637a365990:current
[0%] start: Publishing 84802efd57956051fbe7d3165489afea727465705735bf90deb120efc6c774e5:current
[0%] start: Publishing ec2ff3a73daf647627f95881ab698bb2bb6302a917c4716b1a7baf7338e2ed7d:current
[33%] success: Published 86bb9646ec2db1228e0311c14da31648235c91b989b962349fa001637a365990:current
[66%] success: Published ec2ff3a73daf647627f95881ab698bb2bb6302a917c4716b1a7baf7338e2ed7d:current
[100%] success: Published 84802efd57956051fbe7d3165489afea727465705735bf90deb120efc6c774e5:current
CdkDayStack: creating CloudFormation changeset...

 ✅  CdkDayStack

✨  Deployment time: 162.23s

Outputs:
CdkDayStack.APIurl = https://7it2aofnci.execute-api.us-east-1.amazonaws.com/
CdkDayStack.GetFunctionName = CdkDayStack-GetTranslationFunction0677F2E3-7PvCDYJopsP0
CdkDayStack.PutFunctionName = CdkDayStack-PutTranslationFunction9E955411-AHBOoLMBlumO
CdkDayStack.SaveFunctionName = CdkDayStack-SaveTranslationFunctionD9E440D6-RDudAb44XUcn
CdkDayStack.TranslationBus = TranslateBus
CdkDayStack.TranslationTable = CdkDayStack-TranslateTable1ABF9811-15TOF7OSYIFMJ
Stack ARN:
arn:aws:cloudformation:us-east-1:312512371189:stack/CdkDayStack/9e374010-67a1-11ed-88f8-0a483577940f

✨  Total time: 162.29s
```

After deploying this stack with the AWS CDK, copy info from the outputs (_example_ above) to create a `locals.json` file in the root project directory with the following structure:
```
{
  "CdkDayStack/GetTranslationFunction": {
    "TRANSLATE_TABLE": "CdkDayStack-TranslateTable1ABF9811-15TOF7OSYIFMJ"
  },
  "CdkDayStack/PutTranslationFunction": {
    "TRANSLATE_BUS": "TranslateBus"
  },
  "CdkDayStack/SaveTranslationFunction": {
    "TRANSLATE_TABLE": "CdkDayStack-TranslateTable1ABF9811-15TOF7OSYIFMJ"
  }
}
```

This file provide environment info that SAM will need to run/test the local api:
```
sam-beta-cdk local start-api -n locals.json
```
