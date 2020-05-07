This repo extends https://github.com/aws-samples/aws-amplify-vue and adds the ability to sign in with Federated providers including Google and Facebook.

# The first step is to install the amplify vue application and configure authentication. You can configure federation from the amplify CLI or through the AWS console. 
# Next, run npm install amplify-vue-social-auth
# The next step is to update the aws-exports.js file in your application. This package makes use the cognito user pool. Federation depends on the oath object. This application adds the socialProviders property to the oath object. Each item in the array will display a login button.

```
const awsmobile = {
    "aws_project_region": "----",
    "aws_cognito_identity_pool_id": "----",
    "aws_cognito_region": "----",
    "aws_user_pools_id": "----",
    "aws_user_pools_web_client_id": "----",
    "aws_appsync_graphqlEndpoint": "----",
    "aws_appsync_region": "----",
    "aws_appsync_authenticationType": "----",
    "aws_user_files_s3_bucket": "----",
    "aws_user_files_s3_bucket_region": "----",
    oauth: {
        domain: '----',
        scope: ['phone', 'email', 'profile', 'openid', 'aws.cognito.signin.user.admin'],
        redirectSignIn: 'http://localhost:8080/callback',
        redirectSignOut: 'http://localhost:8080/',
        responseType: 'code', // or 'token', note that REFRESH token will only be generated when the responseType is code
        socialProviders: ['Google','Facebook' ]
    }
};

export default awsmobile;
```
# The redirects listed are for development. You will need to update them for production
# Next, update src/router/index.js adding 
```
import { SocialAuth,SocialAuthCallback} from 'amplify-vue-social-auth';
```
with the other import statements.

After
```
const router = new Router({
```
add
```  
mode: 'history',
```
Replace the route for /auth and add a route for /callback
```
    {
      path: '/auth',
      name: 'Authenticator',
      component: SocialAuth
    },
    {
      path: '/callback',
      name: 'callback',
      component: SocialAuthCallback
    }
```

A working example is available at
https://github.com/jtpenny/amplify-vue-journal
