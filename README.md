# ksuid-cli

A Command Line Interface for dealing with [Segment's KSUIDs](https://github.com/segmentio/ksuid).

Uses [Mark Wubben's KSUID node.js library](https://github.com/novemberborn/ksuid).

## Installation

```console
$ npm install ksuid-cli
```

This package comes with a simple command-line tool `ksuid`. This tool can
generate KSUIDs as well as inspect the internal components for debugging
purposes.

## Usage examples

### Generate 4 KSUIDs

```sh
> ksuid -n 4
151zKb0yBE31siVu9GYmpi1vlfe
151zKUmtgUA8kRSgg5Q6tG6vqPx
151zKTalsFp5ddmaiEaXu7l3YTD
151zKUVLrYKQ1p6XNDRPIFbrN1w
```

### Inspect the components of a KSUID

Using the inspect formatting on just 1 ksuid:

```sh
> ksuid -f inspect

REPRESENTATION:

  String: 151zOCJ2I9szGtX4VwDJjnmvrpZ
     Raw: 0793CB58A38B910C80235B72A6F6B5DF5CA3C929

COMPONENTS:

       Time: 2018-05-24T01:46:00.000Z
  Timestamp: 127126360
    Payload: A38B910C80235B72A6F6B5DF5CA3C929
```

Using the template formatting on 4 ksuid:

```sh
> ksuid -f template -t '{{ .Time }}: {{ .Payload }}' -n 4
2018-05-24T01:46:31.000Z: B34547537772BBC0E2F29CACFC0BB5C2
2018-05-24T01:46:31.000Z: 79A4B61465263502F6F6B3D686F3B48E
2018-05-24T01:46:31.000Z: DBBF7F076962352AD8D60D45A34F5499
2018-05-24T01:46:31.000Z: B00E173900EBB05D768CADF13C3583D0
```

### Generate detailed versions of new KSUID

Generate a new KSUID with the corresponding time using the time formatting:

```sh
> ksuid -f time -v
151zVo4Jr8dajx0fqHWAPxDbHRs: 2018-05-24T01:47:01.000Z
```

Generate 4 new KSUID with details using template formatting:

```sh
> ksuid -f template -t '{ "timestamp": "{{ .Timestamp }}", "payload": "{{ .Payload }}", "ksuid": "{{.String}}"}' -n 4
{ "timestamp": "127126441", "payload": "AF7BF3D0DB709B7933AF1AE83FBF4FBA", "ksuid": "151zYNlpxMf7nbb8CikaE4SUPQw"}
{ "timestamp": "127126441", "payload": "6E92616BDA6CC1B983D238E496080BAC", "ksuid": "151zYLnLhlehuIEeodZLMQ41c4a"}
{ "timestamp": "127126441", "payload": "8D55A9221F760433347F2B08C597AF3F", "ksuid": "151zYMjOiZv7K8q4dEYYySDpyu7"}
{ "timestamp": "127126441", "payload": "22FB4CB82107AC16628F77F60A5BFFE0", "ksuid": "151zYJUiEi4iniicXeu9xShcm3c"}
```

Display the detailed version of a new KSUID:

```sh
> ksuid -f inspect

REPRESENTATION:

  String: 151zbEzzY29y1EMfAycgv4kZTod
     Raw: 0793CBC06EA61F24424C8C6ED6DD3C7540AB013F

COMPONENTS:

       Time: 2018-05-24T01:47:44.000Z
  Timestamp: 127126464
    Payload: 6EA61F24424C8C6ED6DD3C7540AB013F

```