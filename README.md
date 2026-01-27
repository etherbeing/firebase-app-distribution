# Firebase App Distribution Github Action

Even though this is a Fork, is quite not related to the original one...
I re made it totally because how difficult was to trace the original one, even though I review it, but the issue was too many layers +actions+ci+sh+docker is too much for something that can be done in too many layers... at least for basic usage for my own usage this is enough.

## Usage
You must use `git secret` for hiding your firebase credentials, instead of passing it to this action.
You'll only provide two inputs:
**appId**: The id of your app, probably this will in a future be obtained from one of the firebase generated files
**gpgSecretsKey**: This is very important, is a GPG private key used to encrypt the secrets, please beware that you SHOULD NOT give your own personal or working private key, instead create a safe private key only intended to be used for this project and use `git secret tell` and `git secret hide` to hide the secrets with that private key, after that, give the created private key to your GITHUB secrets and use this actions as follows:
```yml
uses: etherbeing/firebase-app-distribution
with:
  appId: ${{secrets.FIREBASE_APP_ID}}
  gpgSecretsKey: ${{secrets.GPG_PRIVATE_KEY}}
``` 

## Afterwords
If you have any suggestion I'd really be happy to apply it, I aim to focus on privacy and safety while providing this action to the public that's why I reduced the code this much after reviewing the original one.

My concern with the original one was that if not for the sha tag is in theory possible for a bad actor to change the docker image to a malicious one making the credentials to be exposed that's why I'd prefer not using docker at all inside my 3rd party actions.