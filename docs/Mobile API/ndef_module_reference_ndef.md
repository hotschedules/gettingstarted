---
title: "NDEF"
posted: 2014-01-30
post: true
---

# NDEF 

## Overview

The `ndef` object provides NDEF constants, functions for creating NdefRecords, and functions for converting data.

## Tasks

  * `record` function
  * `textRecord` function
  * `uriRecord` function
  * `absoluteUriRecord` function
  * `mimeMediaRecord` function
  * `smartPoster` function
  * `emptyRecord` function
  * `encodeMessage` function
  * `decodeMessage` function
  
## Constants

	// see android.nfc.NdefRecord for documentation about constants
    // http://developer.android.com/reference/android/nfc/NdefRecord.html
    TNF_EMPTY: 0x0,
    TNF_WELL_KNOWN: 0x01,
    TNF_MIME_MEDIA: 0x02,
    TNF_ABSOLUTE_URI: 0x03,
    TNF_EXTERNAL_TYPE: 0x04,
    TNF_UNKNOWN: 0x05,
    TNF_UNCHANGED: 0x06,
    TNF_RESERVED: 0x07,


    RTD_TEXT: [0x54], // "T"
    RTD_URI: [0x55], // "U"
    RTD_SMART_POSTER: [0x53, 0x70], // "Sp"
    RTD_ALTERNATIVE_CARRIER: [0x61, 0x63], // "ac"
    RTD_HANDOVER_CARRIER: [0x48, 0x63], // "Hc"
    RTD_HANDOVER_REQUEST: [0x48, 0x72], // "Hr"
    RTD_HANDOVER_SELECT: [0x48, 0x73], // "Hs"
  
## Functions

### record

`ndef.record( tnf, type, id, payload )`

#### Discussion

Creates a JSON representation of a NDEF Record.

#### Arguments

* _tnf_required

3-bit TNF (Type Name Format) - use one of the TNF_* constants
   
* _type_required

byte array, containing zero to 255 bytes, must not be null
   
* _id_required
 
byte array, containing zero to 255 bytes, must not be null
   
* _payload_required
 
byte array, containing zero to (2 ** 32 - 1) bytes, must not be null

#### Return Value

  * JSON representation of a NDEF Record.

### textRecord

Helper that creates an NDEF record containing plain text.

#### Discussion

`ndef.textRecord( text, languageCode, id )`

#### Arguments

* _text_required
 
String of text to encode
     
* _languageCode_optional
 
ISO/IANA language code. Examples: “fi”, “en-US”, “fr- CA”, “jp”.
     
* _id_optional
 
byte array, containing zero to 255 bytes

#### Return Value

  * JSON representation of a NDEF Record.

### uriRecord

Helper that creates a NDEF record containing a URI.

#### Discussion

`ndef.uriRecord( uri, id )`

#### Arguments

* _uri_required
 
String represents URI

* @id_optional

byte array, containing zero to 255 bytes

#### Return Value

  * JSON representation of a NDEF Record.

### absoluteUriRecord

Helper that creates a NDEF record containing an absolute URI.
An Absolute URI record means the URI describes the payload of the record.
For example a SOAP message could use "http://schemas.xmlsoap.org/soap/envelope/"
as the type and XML content for the payload.
Absolute URI can also be used to write LaunchApp records for Windows.
See 2.4.2 Payload Type of the NDEF Specification
http://www.nfc-forum.org/specs/spec_list#ndefts
Note that by default, Android will open the URI defined in the type
field of an Absolute URI record (TNF=3) and ignore the payload.
Windows do not open the browser for TNF=3.
To write a URI as the payload use ndef.uriRecord(uri)

#### Discussion

`ndef.absoluteUriRecord( uri, payload, id )`

#### Arguments

* _uri_required
 
String represents URI

* _payload_optional
 
byte array, containing zero to (2 ** 32 - 1) bytes

* @id_optional

byte array, containing zero to 255 bytes

#### Return Value

  * JSON representation of a NDEF Record.

### mimeMediaRecord

 Helper that creates a NDEF record containing an mimeMediaRecord.

#### Discussion

`ndef.mimeMediaRecord( mimeType, payload, id )`

#### Arguments

* _mimeType_required
 
Mime type

* _payload_optional
 
byte array, containing zero to (2 ** 32 - 1) bytes

* @id_optional

byte array, containing zero to 255 bytes

#### Return Value

  * JSON representation of a NDEF Record.

### smartPoster

Helper that creates an NDEF record containing an Smart Poster.

#### Discussion

`ndef.smartPoster( ndefRecords, id )`

#### Arguments

* _ndefRecords_required
 
array of NDEF Records
     
* _id_optional

byte array, containing zero to 255 bytes

#### Return Value

  * JSON representation of a NDEF Record.
  
### emptyRecord

Helper that creates an empty NDEF record.

#### Discussion

`ndef.emptyRecord()`

#### Return Value

  * JSON representation of a NDEF Record.

### encodeMessage

Encodes an NDEF Message into bytes that can be written to a NFC tag.

#### Discussion

`ndef.encodeMessage( ndefRecords )`

#### Arguments

* _ndefRecords_required
 
array of NDEF Records

#### Return Value

  * byte array ( see NFC Data Exchange Format (NDEF) http://www.nfc-forum.org/specs/spec_list/ )

### decodeMessage

Decodes an array bytes into an NDEF Message

#### Discussion

`ndef.decodeMessage( bytes )`

#### Arguments

* _bytes_required

an array bytes read from a NFC tag

#### Return Value

  * array of NDEF Records ( see NFC Data Exchange Format (NDEF) http://www.nfc-forum.org/specs/spec_list/ )

* * *

(C) 2014 Red Book Connect. All rights reserved. (Last updated: 2014-10-28)
