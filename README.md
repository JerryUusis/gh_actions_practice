# Github actions practice

## Install Nektos `act` to run workflows locally

Navigate to [https://nektosact.com/usage/index.html](https://nektosact.com/usage/index.html) and follow instructions how to run install Nektos Act on your device. It will allow you to run github actions locally, so you can test them without doing a push to your repository every time you want to test you actions. NOTE: You need to have Docker installed on your device. `act` will create an image where an environment is simulated.

Once installed, type `act` in the terminal to emulate a push action to your repository.

## Making Github Actions work

Install following dependencies

 ESLint for linting the code:
 ```shell
 npm init @eslint/config
 ```

 Jest for unit testing:
 ```shell
 npm install jest --save-dev
 ```

 It's also highly recommended to install types for Jest

 ```shell
npm install @jest/types
```

Update package.json linting script. ESLint will lint files with .ts (TypeScript) and .tsx (TypeScript React) extensions. One of the jobs is using this script to lint the code.

```json
"scripts": {
    "lint": "eslint . --ext ts,tsx --report-unused-disable-directives --max-warnings 0 --fix",
}
```

Update eslint.cjs. This will make sure linting works in also in the testing environment with jest. you also want these folders ignored by eslint.

```js
env: { jest:true },
ignorePatterns: ['dist', '.eslintrc.cjs', '.github'],
```

## Repository secrets

Repository secrets are hidden variables that are used by Github actions. You can use them to integrate Github Actions with 3rd party services such as SonarCloud or Netlify. Github repo has it's own default secret `secrets.GITHUB_TOKEN` that is used to identify the repository.

Repository secrets are set under settings > Secrets and variables > actions

### SonarCloud

If you want to automate SonarCloud scan you need to set `SONAR_TOKEN` as a secret in the repository. 

You can get this by connecting our repo with Sonarcloud and choosing GitHub Actions as the Analysis method. 

### Netlify

If you want to automate deployment to Netlify, you need to set `NETLIFY_AUTH_TOKEN` and `NETLIFY_SITE_ID` as repository secrets. 

You need to also connect Netlify with your repository so you can get an access to these values and then save them as secrets.