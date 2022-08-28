- 👋 Hi, I’m @SgL-aYa811p
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
SgL-aYa811p/SgL-aYa811p is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

@Override
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);

    setContentView(R.layout.activity_login);

    Auth0 account = new Auth0(getString(R.string.com_auth0_client_id), getString(R.string.com_auth0_domain));
    auth0Client = new AuthenticationAPIClient(account);

    fbCallbackManager = CallbackManager.Factory.create();

    LoginButton loginButton = findViewById(R.id.login_button);
    loginButton.setPermissions(FACEBOOK_PERMISSIONS);
    loginButton.registerCallback(fbCallbackManager, new FacebookCallback<LoginResult>() {
        @Override
        public void onSuccess(LoginResult result) {
            //1. Logged in to Facebook
            AccessToken accessToken = result.getAccessToken();
            performLogin(accessToken);
        }

        @Override
        public void onCancel() {
            //User closed the dialog. Safe to ignore
        }

        @Override
        public void onError(FacebookException error) {
            //Handle Facebook authentication error
        }
    });
}
