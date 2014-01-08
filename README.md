File uploader for Deployd [![NPM](https://nodei.co/npm/dpd-fileupload.png?compact=true)](https://npmjs.org/package/dpd-fileupload/)
=========================

###This module is higly unstable, use it at your own risk.

Module for Deployd to upload files.  
Upload the files to a local folder (currently in the public folder to access them) and store the filenames in a collection.


Don't hesitate to [fill an issue](https://github.com/NicolasRitouet/dpd-fileupload/issues/new) if you find a bug or need a feature.



Installation
------------

Go to the base directory of your Deployd project and enter:

    npm install dpd-fileupload --save


Configuration
-------------
You have to create a directory in the "public" directory of your project (default is "upload") and set its name into the dashboard settings.

Usage
-----
### Upload a file
Method POST or PUT (set content type to "multipart/form-data"), send "subdir" as request param to save the file in a sub directory

Working demo available here: https://github.com/NicolasRitouet/dpd-fileupload-demo

### Get the list of files
Method GET

    dpd.fileupload.get(function(err, result) {
        console.log(result);
    });

### Get one file
Since we upload the files into the /public folder, you can access your files like this:
http://localhost:2403/upload/subdir/filename.extension
replace:
- upload by the folder your set in the dashboard
- subdir by the value you set for subdir. (nothing if you haven't given a subdir param)
- filename.extension by the name of the file your uploaded

If you would like more security and some rights management to get the files, [fill an issue](https://github.com/NicolasRitouet/dpd-fileupload/issues/new) about this and I might work on this feature.


### Remove a file from filesystem and from collection
Method DELETE

    dpd.fileupload.delete(id, function(err, result) {
        if (err) alert(err);
        console.log(result);
    });

Notes
-----
Currently, you have to set the content type to "multipart/form-data".  
GET of one item is planned. That would allow us to remove the upload directory from public and stream the files and increase security by adding some restrictions.

Todo
----
- add tests
- improve demo
- add optional creatorId property and optional comment property
- check if file already exist (upload anyway and put a (1) in the filename or throw an error?)
- Response after upload is returned too soon, uploaded file is not in the returned response (add a "remainingFile" integer)
- Find a cleaner way to get the path of the upload directory
- Implement GET of one file (stream file ?)
