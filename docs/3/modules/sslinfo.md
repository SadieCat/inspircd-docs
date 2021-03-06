---
title: "Module Details: sslinfo (v3)"
---

## The "sslinfo" Module

### Description

This module adds user facing TLS (SSL) information, various TLS (SSL) configuration options, and the `/SSLINFO` command to look up TLS (SSL) certificate information for other users.

### Configuration

To load this module use the following `<module>` tag:

```xml
<module name="sslinfo">
```

#### `<connect>`

This module extends [the core `<connect>` tags](/3/configuration#connect) with the following fields:

Name       | Type | Default Value | Description
---------  | ---- | ------------- | -----------
requiressl | Text | no            | Whether users must be using TLS (SSL) to use this class.

The requiressl field should be set to one of the following values:

Value   | Description
------- | -----------
no      | TLS (SSL) is not required to use this class.
trusted | TLS (SSL) is required and and a CA-verified client certificate must be provided to use this class.
yes     | TLS (SSL) is required to use this class.

##### Example Usage

Requires users to be using TLS (SSL) to be assigned to the Secure class:

```xml
<connect name="Secure"
         ...
         requiressl="yes">
```

#### `<oper>`

This module extends [the core `<oper>` tag](/3/configuration#oper) with the following fields:

Name        | Type    | Default Value | Description
----------- | ------- | ------------- | -----------
autologin   | Boolean | No            | Whether to automatically log server operators in when they connect to the server.
fingerprint | Text    | *None*        | If defined then a space-delimited list of fingerprints of this server operator's TLS (SSL) client certificates.
sslonly     | Boolean | No            | Whether this server operator must be connected using TLS (SSL) to log into their account.

##### Example Usage

```xml
<oper name="Sadie"
      ...
      autologin="no"
      fingerprint="5d7499e1a3537687a2e875fed60b171508a4d1384351e276c4f961ab80729249"
      sslonly="yes">
```

#### `<sslinfo>`

The `<sslinfo>` tag defines settings about how the sethost module should behave. This tag can only be defined once.

Name     | Type    | Default Value  | Description
-------- | ------- | -------------- | -----------
operonly | Boolean | No             | Whether user TLS (SSL) certificate fingerprints are only visible to server operators.

##### Example Usage

```xml
<sslinfo operonly="no">
```

### Commands

Name    | Parameter Count | Syntax     | Description
------- | --------------- | ---------- | -----------
SSLINFO | 1               | `<target>` | Views the TLS (SSL) certificate information for &lt;target&gt;.

#### Example Usage

Views the TLS (SSL) certificate information for Sadie:

```plaintext
/SSLINFO Sadie
```

[**New in v3.9.0!**](/3/change-log/#inspircd-390) Views the TLS (SSL) certificate information for users in #wibble:

```plaintext
/SSLINFO #wibble
```

### Special Notes

{! 3/modules/_ssl_table.md !}
