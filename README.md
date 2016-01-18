﻿MEGA Web client
=====

MEGA provides robust cloud storage with convenient and powerful always-on privacy. MEGA believes in your right to privacy and provides you with the technology tools to protect it. We call it User Controlled Encryption, or UCE, and it happens automatically.

Secure Boot
-----

secureboot.js loads all the resources from static content servers and verifies its authenticity by checking the cryptographic hash.

*Please note that this is not the exact same secureboot.js as we have online at https://mega.nz/secureboot.js. We have an automatic process that generates secureboot.js with its cryptographic hashes and all the versioned resource files (file_X.js / file_X.html) as needed based on this repository before prior to updating the live site.*

During development it's essential that your set the following localStorage parameters:
```
localStorage.staticpath = 'http://localhost/mega/';    // path of your local development host
localStorage.dd = 1;	// disables the cryptographic hash verification logic
```
There are also various other localStorage parameters that are useful during development:
```
localStorage.d = 1;		// enables vanilla console logging
localStorage.minLogLevel = 0;	// enables full console logging via MegaLogger
localStorage.contextmenu = 1;	// allows you to disable the contextmenu in the FM for element inspection
```

Setup
----
Since 29 Jul, 2014, now the webclient requires "npm" (please follow the instructions for installing from npmjs.org) and
after the initial clone/pull/update of the code from the repo, you would need to always run:
``npm install``, which will guarantee that you have the latest npm packages installed.

Its important to run this command after you pull changes from the repo, because the actual package.json may had been
changed.

Development VS Demo/Beta VS Production environments
-----
Since we'd added React to our toolkit (because of the needs and requirements added by the MegaChat), there is this new
file: ``js/chat/bundle.js``, which is not available in the repository.

This file is generated by ``webpack`` (don't worry about what it does at the moment) and depending on the environment
you may use 2 different methods to generate it.

1) Development environment. Its best to simply use ./dev_server.js, which would NOT generate the file on your file
system, but serve it from memory. This makes the compiling/development a lot more faster and adds some features as hot
reload (e.g. will reload PROPERLY all JSX related code, not .JS, only .JSX and update the UI with the changes...)

2) Demo/beta environments. Those are mostly used for demoing something internally or on beta.mega.nz. This type of
deployment is basically done after cloning the specific/target feature branch on webserver via ssh and then doing:
``npm install && ./build.sh``.

    When doing updates to that folder on the server, just do a:
    ``git pull -u && npm install && ./build.sh``

    Also note, that the webclient will also require some localStorage variables set so that it works as expected, as:
    ```
    localStorage.d = 1;
    localStorage.dd = 1;
    localStorage.jj = 1;
    localStorage.jjnocache = 1; /* added recently by Diego, when set will add a ?r=Date() to enforce browser cache to
                                    be disabled */
    ```
3) Live environment. I've no idea how we are doing live deployments, so please contact @Chris or ask in #webclient.


Directories
-----

**js/** contains all generic JavaScript files

**html/** contains all generic HTML files

**js/html/** contains all JavaScript files that belong to the specific HTML file of the parent folder


JavaScript files
-----

**asmcrypto.js** general-purpose cryptographic library

**secureboot.js** loads all the resources from static content servers and verifies its authenticity by checking the cryptographic hash

**decrypter.js** the decrypter which is used as a web worker to decrypt data while downloading

**encrypter.js** the encrypter which is used as a web worker to encrypt data while uploading

**js/arkanoid.js** has the arkanoid game which is used to collect entropy for public/private key creation

**js/avatar.js** is used for avatar selection, cropping & scaling (all on the client side in the canvas)

**js/base64.js** base64 library

**js/checkboxes.js** jQuery iOS styled checkboxes

**js/cleartemp.js** contains clearIt() which is used to purge temp data from the FileSystem API (Chrome only)

**js/countries.js** contains all the country names (we should translate these at some point)

**js/crypto.js** contains all the cryptographic functions & API handlers

**js/download.js** contains all the download logic

**js/exif.js** library that we use to read the EXIF flags from images prior to client side thumbnail creation

**js/filedrag.js** event handlers for the upload buttons, file&folder-drag&drop event handling for upload init.

**js/filetypes.js** contains all the supported file types based on the file extension to match icons

**js/fm.js** file manager core file, contains mainly file manager UI & dialog UI logic

**js/functions.js** contains some generic functions that are used throughout the site

**js/hex.js** HEX conversion functions

**js/jquery.jscrollpane.js** jScrollpane jQuery plugin for custom scrollbars

**js/jquery.mousewheel.js** jQuery mousewheel plugin for cross browser mousewheel event handling

**js/jquery-2.1.1.js** jQuery library

**js/jquery-ui-1.11.2.js** jQuery User Interface for various UI functionallity, such as: rubberband selection, drag&drop

**js/json.js** provides JSON.parse & JSON.stringify to older browsers

**js/keygen.js** for cryptographic public/private key pair creation

**js/mDB.js** providers the local database abstraction layer for caching of metadata in IndexedDB

**js/mega.js** MegaData class which does most of the datahandling (but also some FM UI interaction)

**js/megapix.js** client side canvas based thumbnail creation (because thumbnails are encrypted, too)

**js/mouse.js** captures mouse events for entropy collection

**js/notify.js** contains the notifications logic

**js/rsa.js** cryto library for RSA

**js/thumbnail.js** client side canvas based thumbnail creation (because thumbnails are encrypted, too)

**js/upload.js** contains all the upload logic

**js/user.js** contains the user creation & login logic

**js/zip.js** JavaScript implementation to create ZIP archives of multiple files on the client side

**js/zxcvbn.js** password strength verification library (including dictionary table)

