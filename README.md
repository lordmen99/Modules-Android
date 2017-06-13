#Hasura Android Module - Login

This module portrays different ways in which you can use Hasura Auth for SignUp and Login.

##Configuring the Hasura Android SDK:

Once you have created your android project, you will have to add [Hasura-Android SDK](https://github.com/hasura/android-sdk). 
For doing this please refer the README at 

##OTP SignUp and Login:

For using mobile OTP SignUp and Login, you will first have to enable mobile verification in the console and create an account on MSG91.
Following is a link to a blogpost for setting up mobile verification and MSG91:
// Blogpost for MSG91 link here.

###OTP SignUp:
Step 1: 
  Create a new HasuraUser object(say "user") and initialize it.
  ```
  Final HasuraUser user = new HasuraUser();
  
  ```
  
Step2: 
  When the signUp button is clicked,use
  user.setMobile(mobilenumber) to set the mobile number.
  Then call the user.signup() to request otp.
  
  ```
  user.signUp(new AuthResponseListener() {
                    @Override
                    public void onSuccess(HasuraUser hasuraUser) {
                        
                    }

                    @Override
                    public void onFailure(HasuraException e) {
                        
                    }
                });
  
  ```
Step3:
  On success, it the OnSuccess() method, receive the otp.
  Then call user.confirmMobile(otp,MobileConfirmationResponseListener) to confirm the otp.
  
  ```
  user.confirmMobile(otp.getText().toString(), new MobileConfirmationResponseListener() {
                                    @Override
                                    public void onSuccess() {
                                        
                                    }

                                    @Override
                                    public void onFailure(HasuraException e) {
                                    
                                    }
                                });
  
  ```
Step4:
  On success, you will receive the auth token and hasura-id in the response.
  
###OTP Login:
Step 1:
  Create a new HasuraUser object(say "user") and initialize it.
Step 2:
  When loginbutton is clicked, use
  user.setMobile(mobilenumber) to set the mobile number.
Step 3:
  Call user.enableMobileOtpLogin() to enable LogIn using OTP.
  
  ```
  user.setMobile(mobile.getText().toString());
  user.enableMobileOtpLogin();
  
  ```
  
Step 4:
  Call user.sendOtpToMobile(OtpStatusListener) to send OTP to mobile.
  
  ```
  user.sendOtpToMobile(new OtpStatusListener() {
                    @Override
                    public void onSuccess() {

                    }

                    @Override
                    public void onFailure(HasuraException e) {
                        
                    }
                });
  
  ```
    (Currently there is a slight is issue with the sendOtpToMobile() API, it will give a 401 and then send the OTP.
    This will be fixed soon, for the time being you can call the confirmMobile() in the onFailure() to make it work) 
    
Step 5:
  If the above step is successful, you will receive the otp.
  Receive this otp and call user.confirmMobile(otp,MobileConfirmationRequest) to confirm the otp.
  
Step 6:
  On success, you will receive the auth token and hasura-id in the response.
