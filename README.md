��#   b o n t y 
 
 Here is a step-by-step guide on integrating Immutable Passport into an application:

Guide: Integrate Immutable Passport into your Application
1. Create a simple application
You can start a new Node.js project or clone an example repo.



git clone https://github.com/immutable/sdk-examples
cd sdk-examples/passport
npm install
This gives you a basic Express app to start with.

2. Register the application
Go to the Immutable Developer Hub and create a new application. Under Passport settings, create a new client.

Take note of the clientId, redirectUri and logoutRedirectUri.

3. Install and initialize Passport
Install the Passport SDK:

Copy code

npm install @imtbl/sdk
Then initialize Passport with your client details:

js

Copy code

const passport = new Passport({
  clientId: '...',
  redirectUri: 'http://localhost:3000/callback',
  // ...
});
4. Enable user login
To log users in, call passport.connectIMX() which opens the login popup.

Handle the redirect in the callback route:

js

Copy code

// Login route
app.get('/login', async (req, res) => {
  await passport.connectImx();
});

// Callback route 
app.get('/callback', (req, res) => {
  passport.loginCallback(); 
});
5. Display user information
After login, you can display user data like:

js

Copy code

const idToken = await passport.getIdToken();
const nickname = await passport.getUserInfo().nickname;
6. Log out users
To log users out, call:

js

Copy code

await passport.logout();
7. Initiate a transaction
To send a transaction:

js

Copy code

const provider = await passport.connectImx();

const tx = await provider.transfer({
  type: TransferType.WITHDRAWAL, 
  amount: '0x1',
  tokenId: '...' 
});

console.log(tx.hash);
This shows the key steps to add Passport authentication and wallet interactions. Let me know if you need any clarification!
