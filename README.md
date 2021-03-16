# LastFM Station Providers

These scripts provide metadata about currently playing tracks to
the [lastfm script][lastfm].

[lastfm]: https://github.com/nanont/scripts/blob/master/lastfm

## Protocol

To ease the creation of new providers and let implementors choose any
language they want, providers are expected to adhere to the following
protocol:

- Emit relevant information via `STDOUT` as `UTF-8`
- Line 1 consists of one of three statuses `OK | SKIP | ERROR`
  - `OK`: Track can be submitted. Line 2 contains the artist. Line 3
    contains the title.
  - `SKIP`: Do not submit this track. Additional (non-standardised)
    information might follow.
  - `ERROR`: Something went wrong. Additional (non-standardised)
    information might follow.
- Emit anything else or unrelated on `STDERR`

Also, providers should execute as fast as possible and refrain from
manipulating files, interacting with the OS more than necessary, etc.

### Examples

#### OK

Return code: 0

Printed to STDERR:
```
OK
Lush
De-Luxe
```

#### SKIP

Return code: 0

Printed to STDERR:
```
SKIP
$VAR1 = {
          'duration' => 141500,
          'endISO' => '2021-03-16T13:13:41+01:00',
          'start' => '1615896680000',
          'type' => 'M'
};
```

#### ERROR

Return code: -1

Printed to STRERR:
```
ERROR
404
```
