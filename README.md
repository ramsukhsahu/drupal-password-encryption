# drupal-password-encryption
Password Encryption for Drupal 10
Overview
This module provides client-side encryption of the user password during the Drupal login process.

The implementation is based on the Drupal Password Encrypt module.

When a user submits the Drupal login form, the password is encrypted in the browser before it is sent to the Drupal server. The username is submitted normally.

Login Flow
User
  |
  | Username + Password
  v
Drupal Login Form
  |
  | Encrypt Password
  v
Encrypted Password + Username
  |
  | Submit to Server
  v
Drupal Server
  |
  | Decrypt Password
  v
Drupal Authentication
  |
  v
Login Success / Failure

Features
Encrypts the password before login form submission.

Username remains unchanged.

Uses client-side JavaScript encryption.

Based on the Drupal Password Encrypt module.

Integrates with the Drupal login form.

Allows the decrypted password to be passed to Drupal's normal authentication process.

Does not change Drupal's normal password storage and hashing mechanism.

Requirements
Drupal 10

PHP version supported by the installed Drupal 10 version

JavaScript enabled in the browser

CryptoJS/AES library, if required by the implementation

HTTPS/TLS enabled on the website

Installation
1. Install the module
Place the module in the Drupal custom modules directory:

web/modules/custom/password_encrypt/

Alternatively, install it using Composer if your project is configured for Composer-based installation.

2. Enable the module
Using Drush:

drush en password_encrypt -y

Clear the Drupal cache:

drush cr

The module can also be enabled from:

Administration → Extend

How Password Encryption Works
The password is entered normally by the user:

Password:
MyPassword123

Before the login form is submitted, JavaScript encrypts the password:

MyPassword123
      |
      v
Client-side encryption
      |
      v
Encrypted password

The encrypted password is then submitted to the Drupal server.

The server-side implementation decrypts the password before Drupal performs the normal authentication process.

Example
Before Encryption
Username: admin
Password: MyPassword123

Submitted Request
Username: admin
Password: <encrypted-password>

The actual encrypted value will depend on the encryption algorithm, key, IV, and implementation configuration.

Password Authentication Flow
1. User opens /user/login
              |
              v
2. User enters username and password
              |
              v
3. User submits login form
              |
              v
4. JavaScript encrypts password
              |
              v
5. Encrypted password is submitted
              |
              v
6. Drupal receives username + encrypted password
              |
              v
7. Password is decrypted
              |
              v
8. Drupal validates the credentials
              |
              v
9. User is logged in

Username Handling
This implementation encrypts only the password.

The username is not encrypted.

Username  → Sent normally
Password  → Encrypted before submission

Example:

Username: admin
Password: <encrypted-value>

Drupal Password Storage
This module should not store plaintext passwords.

The purpose of the encryption is to protect the password during the login submission process.

Drupal remains responsible for normal password verification and secure password storage.

The architecture is:

Browser
   |
   | Encrypted password
   v
Drupal
   |
   | Decrypt password
   v
Drupal Authentication
   |
   | Password verification
   v
User Account
