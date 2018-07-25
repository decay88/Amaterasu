# Amaterasu
Amaterasu is a lightweight licensing library for .NET applications which allows the managing of licenses via web based scripts and on-the-fly code compilation. The library also includes common encryption and hashing algorithms such as AES and SHA to ensure that data is protected when communcating with the licensing server; however, since runtime code compilation is available, all methods currently used for licensing can be replaced with custom written modules instead of utilizing the prebuilt licensing structure.

### Requirements
- .NET Framwork 4.6.1

# Features
- Activate and manage license files using web scripts
- Generate C# code in-memory
- Call managed assembly methods and cast types
- Secure communcation between server and client
- Create blacklists from arrays or from a `*NetRequest*`
- Manage the local filesystem using both managed and native methods
- Built-in anti-debugging checking
- User privilege enumeration
- System search (finds and removes blacklisted files from the system)
- Encryption, hashing, and cryptographically strong data generation
    ###### Encryption
    - AES
    
    ###### Hashing
    - MD5
    - RIPEMD160
    - SHA-1
    - SHA-256
    - SHA-384
    - SHA-512
    
# Examples
### License Activation

In order to utilize the license activation methods you must first write two scripts for both validating data as well as one for actually handling the updating and activation of license files; the library uses **POST** requests, usually sent to PHP scripts, which handle all of the server side calculations and managing. The first script is known as the *`Verification Script`* and the second is recognized as the *`Support Script`*. Here's how they are meant to be used:

```c#
using System;
using Amaterasu;

namespace Example
{
    class Program
    {
        static void Main(string[] args)
        {
            // Read a RSA public key to be used for decrypting the license and validating data.
            string publicKey = File.ReadAllText("PathToPublicKey");

            // Read the license file to activate.
            string licenseFile = File.ReadAllText("PathToLicense");

            // Set the username and password that were used at the time of generating the license.
            string username = "someusername";
            string password = "somepassword";

            // Create a new licensing object with our script urls and try activating a license.
            string verifcationScript = "https://www.yourwebsite.com/verification.php"; // Change this to your website.
            string supportScript = "https://www.yourwebsite.com/support.php"; // Change this to your website.
            Licensing manager = new Licensing(verifcationScript, supportScript);
            if (manager.ActivateLicense(publicKey, username, password, licenseFile))
                Console.WriteLine("The license has successfully been activated!");
            else
                Console.Writeline("The license could not be activated.");

            // Wait for user response.
            Console.Read();
        }
    }
}
```
### Dynamic Code Compilation

``` TODO: Finish readme...```

Since Amaterasu has the ability to compile C# on-the-fly the code above can be modified to behave differently without actually modifying the library source. Using this feature in conjuction with the availble features in the library facilitates the possibility of creating a unique licensing schema by writing multiple modules and compiling them as need within a method. An example of this would be to have code check certain aspects of a license file which in turn references another runtime compiled module to actually do any activation or managing of said license. Shown below is a example of compiling an *AMC* or *Authentication Module Chain* that decodes a license, reroutes data validation scripts, and activates the license:


The main namespace which will encapsulate the following code will be: `namespace Dynamic`

###### Encoding Module
```c#
// This module controls the encoding process of a license file.
```

###### Scripting Module
```c#
// This module provides an interface for validating and chunking data.
```
###### Activation Module
```c#
// This module allows an alternative way to activate a license file.
```

---

#### Module Compilation & Use
```c#
// This is an example of compiling the above modules and running them in sequence.
```
##### Singular Compilation
```c#
// Some code here...
```

##### Chain Compilation
```c#
// Some code here...
```
