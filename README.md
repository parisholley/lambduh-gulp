# lambduh-gulp
A handful of gulp commands typical to building AWS Lambda functions

# Usage

```
npm i --save-dev lambduh-gulp
```

Pass your instance of gulp into lambduh-gulp somewhere in your `gulpfile.js`.

```
//gulpfile.js
var gulp = require('gulp');
var lambduhGulp = require('lambduh-gulp');

lambduhGulp(gulp);
```

Optionally, you don't need to require your own `gulp`... but if you want to add any of your own tasks, you'll want your own instance.

# Gulp tasks

## `gulp zipload`

The task you'll use the most – runs `gulp lambda-zip`, then `gulp upload`. See the next two funcs for details.

## `gulp lambda-zip`

- Runs a `clean` to remove any `dist/*` or `dist.zip`
- Pipes your `index.js`, `bin/*`, and `package.json` into a `dist` folder
- Installs your production node-modules in `dist/`
- Zips it up into a `dist.zip`

## `gulp upload`

- Creates and uploads a new Lambda function. If one exists, this will update the function's configuration, then re-upload the latest code. 

This function assumes you have a local `./lambda-config.js` file with details on your lambda function. The parameters match those used by the JS aws-sdk (at the time of writing this):

```
//lambda-config.js
module.exports = {
  FunctionName: 'funcName',
  Description: 'descrip',
  Handler: 'index.handler',
  Role: 'arn:aws:iam:etcetc',
  Runtime: 'nodejs',
  MemorySize: 320,
  Timeout: 60
}
```

Uploading also assumes your have permissions to update lambda functions from your machine. This takes time to configure via the [AWS CLI](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-set-up.html), but the resulting workflow is well worth it in my experience. And besides, AWS's interface is much easier to use from the commandline relative to the non-sense they present in the console.

# Reach out!

I'd love some feedback/PRs/whatever - open an issue and let's talk.
