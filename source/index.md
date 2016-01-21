---
title: Gro APIs

language_tabs:
  - iOS


toc_footers:
  - <a href='http://www.grobanking.com/contact-gro/'>Contact Gro</a>
  - <a href='https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html#//apple_ref/doc/uid/TP40007072-CH6-SW1'>Apple URL Schemes Programming Guide</a>

includes:
  - errors

search: true
---

# Target Audience

This API is intended for development resources well versed in mobile application development and integration.


# Introduction

Welcome to the Gro Account Opening Native API!  This document describes the methods that enable you to integrate the Gro Account Opening Native Application to your institutions mobile banking platform.

The areas to the right include code samples.  Currently only iOS integration is supported, but development for Android and Windows Mobile is underway. 

This document details four methods for initializing and opening the Gro Account Opening Native Application.  The primary means of invoking the application through your mobile banking platform is through the use of a registered url scheme.  The Gro application is installed with the registered scheme "groacct://".

For details on inter-app communication using url schemes, please visit the App Programming Guide for iOS.


# Initialize Gro Account Opening

## OpenApp

```c++

(void)buttonPressed:(UIButton *)button
{
  NSString *customURL = @"groacct://open.acct";

  if ([[UIApplication sharedApplication] canOpenURL:[NSURL URLWithString:customURL]])
  {
    [[UIApplication sharedApplication] openURL:[NSURL URLWithString:customURL]];
  }
  else
  {
    UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"URL error"
                              message:[NSString stringWithFormat:@"No custom URL defined for %@", customURL]
                              delegate:self cancelButtonTitle:@"Ok" 
                              otherButtonTitles:nil];
    [alert show];
  }

}

```



Open the Gro Account Opening application (nothing pre-populated)


### Sample URL 
`groacct://open.acct?productID=24&productID=122`


##OpenAppWithProducts
Open the Gro Account Opening Native App with specific products pre-selected in the shopping cart.


```c++
 (void)buttonPressed:(UIButton *)button
{
  NSString *customURL = @"groacct://open.acct?productID=24&productID=122";

  if ([[UIApplication sharedApplication] canOpenURL:[NSURL URLWithString:customURL]])
  {
    [[UIApplication sharedApplication] openURL:[NSURL URLWithString:customURL]];
  }
  else
  {
    UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"URL error"
                              message:[NSString stringWithFormat:@"No custom URL defined for %@", customURL]
                              delegate:self cancelButtonTitle:@"Ok" 
                              otherButtonTitles:nil];
    [alert show];
  }

}
```


### Sample URL 
`groacct://open.acct?productID=24&productID=122`

### URL Parameters
Parameter | Description
--------- | -----------
productID | Unique Identifier of a financial product such as a specific bank account


## OpenAppSSONoToken

Open the Gro Account opening app with applicant personal information pre-populated.

If a user is already authenticated through the mobile application, the Gro Account Opening application can be invoked and passed application values that will appear pre-populated in the workflow pages. Free form text values that have spaces should be passed with spaces replaced by %20


```c++
 (void)buttonPressed:(UIButton *)button
{
  NSString *customURL = @"groacct://open.acct?email=bob@example.com?phone=5555555555?Address1=100%20Sesame%20Street";

  if ([[UIApplication sharedApplication] canOpenURL:[NSURL URLWithString:customURL]])
  {
    [[UIApplication sharedApplication] openURL:[NSURL URLWithString:customURL]];
  }
  else
  {
    UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"URL error"
                              message:[NSString stringWithFormat:@"No custom URL defined for %@", customURL]
                              delegate:self cancelButtonTitle:@"Ok" 
                              otherButtonTitles:nil];
    [alert show];
  }

}

```



### Sample URL scheme

`groacct://open.acct?email='bob@example.com?phone=5555555555?Address1=100%20Sesame%20Street`

### URL Parameters

Parameter | Description
--------- | -----------
email | Applicant's email address
phone | Applicant's phone number (digits only, no dashes)
firstName | Applicant's first name
lastName | Applicant's last name
middle | applicants middle name or initial
Address1 | Address 1 line
Address2 | Address 2 line
City | City 
State | State (2 character value)
Zip | Zip Code

## OpenAppSSOWithToken

With this method, A SAML token is passed to the Gro Account Opening Application.
The application will then use the token to communicate with the specified server to retrieve and pre-populate applicant informatoin


```c++
 Place code here
```



### Sample URL scheme

`groacct://thisIsaPlaceHolder`

### URL Parameters

Parameter | Description
--------- | -----------
Place Holder | The below is not accurate
SAML Token | Applicant's email address
Server | hostname of the SSO server



