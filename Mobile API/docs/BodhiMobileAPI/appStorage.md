# App Storage Module Reference

## Overview

This module provides the ability to store any kind of data.  
Developer can add data or strings manually or load files from server.  
Also some modules are supporting to work with **App Storage**. For example
developer can save photo to **App Storage** and then send it as attachment via
email.  
This is simple key-value storage. But value can be a string, a binary data and
a file. The length of value limited only by the size of free memory.

#### Key naming convention

  1. Use a delimiter "/" for separating logic parts of keys.
  2. All modules that store data in **App Storage** use the keys: module_name/generated_id
  3. In order not to damage the data of other embedded applications use keys with prefix app/[your_app_name]

## Tasks

  * `put` function
  * `getAllKeys` function
  * `get` function
  * `delete` function
  * `deleteAll` function
  * `putString` function
  * `getString` function
  * `getStrings` function
  * `putContent` function
  * `loadContent` function
  * `getContent` function

## Functions

### put

`appStorage.put( options, successCallback, errorCallback )`

#### Discussion

With this function developer can save strings, data or file for the key.  
Developer can use this function in three cases:

  1. **Save string data**

For it developer must set key and value properties for _options_

  2. **Save binary data**

For it developer must set key, contentType and data properties for _options_

  3. **Load data from server**

For it developer must set key, url and contentType (optional) properties for
_options_

#### Arguments

  * _options_required

Object with key-value. Supported keys:

    * _key_required

A String value. The key under which data will be stored.

    * _value_

A String value. String data to save.

    * _contentType_

A String value. Content Type of data.

    * _data_

A String value. String data in base64 to save.

    * _url_

A String value. Link to the file on remote server.

  * _succesCallback_optional

Success callback. Called when function finished without errors

Callback parameter is object which contains keys:

    * _key_ \- The key in accordance with which the data was saved. (String)
    * _contentType_ \- Content Type of the data. (String)

  * _errorCallback_optional

Error Callback. Called when function return error.

#### Return Value

  * _[RBCPromise](kernel_promise.html) object_

#### Sample

`appStorage.put( {key:"app/test/key1", value:"Test values"}  
function(info) {  
    alert(info.key + "saved");  
}, function (error) {  
    alert("code: " \+ error.code + "\nmessage: " \+ error.message);  
});`  

### getAllKeys

`appStorage.getAllKeys( options, successCallback, errorCallback )`

#### Discussion

Returns all keys which respond to options.

#### Arguments

  * _options_required

Object with key-value. Supported keys:

    * _prefix_

A String value. The key must contains prefix in the start of string.

    * _contentType_

A String value. Content Type of data must be equal to this.

  * _succesCallback_optional

Success callback. Called when function finished without errors

Callback parameter is object which contains "keys" array with objects with:

    * _key_ \- The key of record. (String)
    * _contentType_ \- Content Type of the data. (String)

  * _errorCallback_optional

Error Callback. Called when function return error.

#### Return Value

  * _[RBCPromise](kernel_promise.html) object_

#### Sample

`appStorage.getAllKeys( {prefix:"app/test/"}  
function(info) {  
    for (var i = 0; i < info.keys.length; i++) {  
        alert("Key: " \+ info.keys[i].key);  
    }  
}, function (error) {  
    alert("code: " \+ error.code + "\nmessage: " \+ error.message);  
});`  

### get

`appStorage.get( options, successCallback, errorCallback )`

#### Discussion

Return value or data in base64 for specified keys

#### Arguments

  * _options_required

Object with key-value. Supported keys:

    * _key_

A String value. The key for which you want to find a record.

    * _keys_

A Array of Strings value. Use this property to select multiple records.

  * _succesCallback_optional

Success callback. Called when function finished without errors

Callback parameter is object which contains "values" array with objects with:

    * _key_ \- The key of record. (String)
    * _contentType_ \- Content Type of the data. (String)
    * _value_ \- This property returned if record contains string value. (String)
    * _data_ \- data in base64 returned if record contains binary data. (String)

  * _errorCallback_optional

Error Callback. Called when function return error.

#### Return Value

  * _[RBCPromise](kernel_promise.html) object_

#### Sample

`appStorage.get( {key:"app/test/key1"}  
function(info) {  
    for (var i = 0; i < info.values.length; i++) {  
        alert("Found data for key: " \+ info.values[i].key);  
    }  
}, function (error) {  
    alert("code: " \+ error.code + "\nmessage: " \+ error.message);  
});`  

### delete

`appStorage.delete( options, successCallback, errorCallback )`

#### Discussion

Delete records for specified keys

#### Arguments

  * _options_required

Object with key-value. Supported keys:

    * _key_

A String value. Delete records with key.

    * _keys_

A Array of Strings value. Use this property to delete multiple records.

  * _succesCallback_optional

Success callback. Called when function finished without errors

Callback parameter is always null.

  * _errorCallback_optional

Error Callback. Called when function return error.

#### Return Value

  * _[RBCPromise](kernel_promise.html) object_

#### Sample

`appStorage.delete( {key:"app/test/key1"}  
function(info) {  
    alert("Key removed");  
}, function (error) {  
    alert("code: " \+ error.code + "\nmessage: " \+ error.message);  
});`  

### deleteAll

`appStorage.deleteAll( options, successCallback, errorCallback )`

#### Discussion

Delete all keys which respond to options.

#### Arguments

  * _options_required

Object with key-value. Supported keys:

    * _prefix_

A String value. The key must contains prefix in the start of string.

    * _contentType_

A String value. Content Type of data must be equal to this.

  * _succesCallback_optional

Success callback. Called when function finished without errors

Callback parameter is always null.

  * _errorCallback_optional

Error Callback. Called when function return error.

#### Return Value

  * _[RBCPromise](kernel_promise.html) object_

#### Sample

`appStorage.deleteAll( {prefix:"app/test/"}  
function(info) {  
    alert("All keys removed");  
}, function (error) {  
    alert("code: " \+ error.code + "\nmessage: " \+ error.message);  
});`  

### putString

`appStorage.putString( key, value, successCallback, errorCallback )`

#### Discussion

This function use put to add string value.

#### Arguments

  * _key_required

A String value. The key under which string value will be stored.

  * _value_required

A String value. String data to save.

  * _succesCallback_optional

Success callback. Called when function finished without errors

Callback parameter is object which contains keys:

    * _key_ \- The key in accordance with which the data was saved. (String)
    * _contentType_ \- Content Type of the data. (String)

  * _errorCallback_optional

Error Callback. Called when function return error.

#### Return Value

  * _[RBCPromise](kernel_promise.html) object_

#### Sample

`appStorage.putString( "app/test/key1", "Test values",  
function(info) {  
    alert(info.key + "saved");  
}, function (error) {  
    alert("code: " \+ error.code + "\nmessage: " \+ error.message);  
});`  

### getString

`appStorage.getString( key, successCallback, errorCallback )`

#### Discussion

This function use get to get string value.

#### Arguments

  * _key_required

A String value. The key for which you want to find a record.

  * _succesCallback_optional

Success callback. Called when function finished without errors

Callback parameter is object which contains "values" array with objects with:

    * _key_ \- The key of record. (String)
    * _contentType_ \- Content Type of the data. (String)
    * _value_ \- This property returned if record contains string value. (String)
    * _data_ \- data in base64 returned if record contains binary data. (String)

  * _errorCallback_optional

Error Callback. Called when function return error.

#### Return Value

  * _[RBCPromise](kernel_promise.html) object_

#### Sample

`appStorage.getString( "app/test/key1",  
function(info) {  
    for (var i = 0; i < info.values.length; i++) {  
        alert("Found data for key: " \+ info.values[i].key);  
    }  
}, function (error) {  
    alert("code: " \+ error.code + "\nmessage: " \+ error.message);  
});`  

### getStrings

`appStorage.getStrings( key, successCallback, errorCallback )`

#### Discussion

This function use get to get multiple string values.

#### Arguments

  * _keys_required

A Array of Strings value. Use this property to select multiple records.

  * _succesCallback_optional

Success callback. Called when function finished without errors

Callback parameter is object which contains "values" array with objects with:

    * _key_ \- The key of record. (String)
    * _contentType_ \- Content Type of the data. (String)
    * _value_ \- This property returned if record contains string value. (String)
    * _data_ \- data in base64 returned if record contains binary data. (String)

  * _errorCallback_optional

Error Callback. Called when function return error.

#### Return Value

  * _[RBCPromise](kernel_promise.html) object_

#### Sample

`appStorage.getStrings( ["app/test/key1", "app/test/key2"],  
function(info) {  
    for (var i = 0; i < info.values.length; i++) {  
        alert("Found data for key: " \+ info.values[i].key);  
    }  
}, function (error) {  
    alert("code: " \+ error.code + "\nmessage: " \+ error.message);  
});`  

### putContent

`appStorage.putContent( key, contentType, data, successCallback, errorCallback
)`

#### Discussion

This function use put to add binary data.

#### Arguments

  * _key_required

A String value. The key under which data will be stored.

  * _contentType_required

A String value. Content Type of data.

  * _data_required

A String value. String data in base64 to save.

  * _succesCallback_optional

Success callback. Called when function finished without errors

Callback parameter is object which contains keys:

    * _key_ \- The key in accordance with which the data was saved. (String)
    * _contentType_ \- Content Type of the data. (String)

  * _errorCallback_optional

Error Callback. Called when function return error.

#### Return Value

  * _[RBCPromise](kernel_promise.html) object_

#### Sample

`appStorage.putContent( "app/test/key2", "text/plain", "VGVzdA==",  
function(info) {  
    alert(info.key + "saved");  
}, function (error) {  
    alert("code: " \+ error.code + "\nmessage: " \+ error.message);  
});`  

### loadContent

`appStorage.loadContent( key, url, successCallback, errorCallback )`

#### Discussion

This function use put to load data from remote server.

#### Arguments

  * _key_required

A String value. The key under which data will be stored.

  * _url_required

A String value. Link to the file on remote server.

  * _succesCallback_optional

Success callback. Called when function finished without errors

Callback parameter is object which contains keys:

    * _key_ \- The key in accordance with which the data was saved. (String)
    * _contentType_ \- Content Type of the data. (String)

  * _errorCallback_optional

Error Callback. Called when function return error.

#### Return Value

  * _[RBCPromise](kernel_promise.html) object_

#### Sample

`appStorage.loadContent( "app/test/key3", "http://www.company.com/file_url",  
function(info) {  
    alert(info.key + "saved");  
}, function (error) {  
    alert("code: " \+ error.code + "\nmessage: " \+ error.message);  
});`  

### getContent

`appStorage.getContent( key, successCallback, errorCallback )`

#### Discussion

This function use get to get binary data in base64.

#### Arguments

  * _key_required

A String value. The key for which you want to find a record.

  * _succesCallback_optional

Success callback. Called when function finished without errors

Callback parameter is object which contains "values" array with objects with:

    * _key_ \- The key of record. (String)
    * _contentType_ \- Content Type of the data. (String)
    * _value_ \- This property returned if record contains string value. (String)
    * _data_ \- data in base64 returned if record contains binary data. (String)

  * _errorCallback_optional

Error Callback. Called when function return error.

#### Return Value

  * _[RBCPromise](kernel_promise.html) object_

#### Sample

`appStorage.getContent( "app/test/key3",  
function(info) {  
    for (var i = 0; i < info.values.length; i++) {  
        alert("Found data for key: " \+ info.values[i].key);  
    }  
}, function (error) {  
    alert("code: " \+ error.code + "\nmessage: " \+ error.message);  
});`  

  * [Index](../index.html)

* * *

(C) 2014 Red Book Connect. All rights reserved. (Last updated: 2014-06-11)

