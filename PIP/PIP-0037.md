<pre>
  PIP: *reserved for PIP editor*
  Title: Title for your PIP
  Type: Protocol | Backend | Front-End | Informational | Process
  Impact: [Hard-Fork|Soft-Fork|None] - [Protcol | API | GUI | Mobile | Other]
  Author: Firstname Lastname <i>&lt;your@email.com&gt;</i>
  Comments-URI: *reserved for PIP editor*
  Status: Draft
  Created: YYYY-MM-DD
</pre>

## Summary

To make the path for a full integration of DATA operations in Pascal with Version 5, it is suggested to create a database of payload protocol specifications to make sure payloads can be identified and parsed correctly based on a concise specification. 

## Motivation

Pascal allows you to add 255 bytes of additional data to be attached with each operation. This is such a powerful feature that the developers implemented another operation type called "DATA Operation". It's sole purpose is to transfer data from account A to account B without necessarily transferring any monetary value. It is also possible to send a DATA operation from account A to account A.

In addition to that, DATA operations can be combined using a unique identifier and a sequence. This means you are able to save more than 255 bytes of data with multiple operations and consecutively concatenate messages later on.

The unique identifier (from now on called channel) is used to group DATA operations, the sequence (from now on called index) is used to sort operations in a way that they can be concatenated in a meaningful way.

Another field in a DATA operation is the data-type, and that is what this PIP is all about. The data-type classifies the data. A client that is reading a DATA operation can identify its payload format and parse it using a specification for the data-type. It's comparable to a mime type or content-type in HTTP.

The Safebox architecture makes it possible for such a feature to not end up in a burden for the users, as to run a Pascal node one just needs the last 100 blocks to be fully operational.

This means normal users are not affected by more DATA operations in Pascal. It can be a burden for perma-node operators to handle the amount of data, but with ongoing research to shard the Pascal blockchain there are solutions on the horizon to also solve this issue. 

This PIP will no further discuss possible scalability problems.

## Specification

While everyone is free to use any data-type for a DATA operation (except 1-1000) and the format of a payload is not enforced on the core protocol level yet, it makes sense to create a database of data-type specifications and it's possible use. Per core protocol definition there are 2^16 data-type specifications possible, enough for a variety of specifications to drive adoption.

The database will map a data-type with a document describing the data format and will be hosted in a git repository, with read access to everyone. New specifications can be added via pull request. This is the most simple solution and should be a good start. It can be expanded in the future.

The documents will also be available via https://data.pascalcoin.org.

### Reserved data-types

There are a number of data types reserved for future use. Some might find it's way into the core protocol, allowing core smart contracts.

#### Data-Type 1-1000

These data-types are reserved for the possible use in Pascal itself and will be enforced by the protocol. There cannot be a specification that is not available in the node software itself. 

**The Pascal node in V5 will reject any DATA operation that uses a data-type of 1-1000.**

#### Data-Type 0

The data-type 0 is reserved as a specification-less data-type. The data-type can be used for any arbitrary data without a specification. This should be the default setting when implementing a client library for Pascal.

#### Data-Type 1001-10000

This data-type simply references a MIME type database introduced and maintained by IANA at https://www.iana.org/assignments/media-types/media-types.xhtml. It will not support every MIME type from the beginning, but the list will evolve. 10000 entries are enough to cover all official MIME types in the next years.

### Specification documentation

A specification will follow a common specification template, just like the PIP template. It should be as precise as possible. The documentation template can be found here (TODO).

It MUST contain the following content:

##### Version
A version number of the format. 

**Version history**

Previous major versions need to be linked by providing the latest stable documentation saved in git. It MUST follow the semver versioning scheme.

##### Block
The block number that identifies the start of the specification, so users can identify the format based on the block the operation was included.

### Formats

The format of a message does not matter. It can be JSON, binary, XML. But with the limited space available, it makes sense to use the most space saving message format. So it is adviced to use any binary specification available.

## Rationale



## Backwards Compatibility

There are no backwards compatibility issues.

## Reference Implementation

None yet.

## Links

References and links to relevant material
