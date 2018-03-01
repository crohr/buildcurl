# buildcurl

Precompiled software, built on demand.

## Usage

    curl buildcurl.com -LGfs \
        --data-urlencode recipe=RECIPE \
        --data-urlencode target=TARGET \
        --data-urlencode version=VERSION \
        --data-urlencode prefix=PREFIX \
        -o output.tgz

`version` and `prefix` are optional. `version` will default to whatever default
version is specified in the `recipe`, and `prefix` defaults to `/usr/local`.

## Supported targets

* ubuntu:16.04
* ubuntu:14.04
* ubuntu:12.04
* debian:8
* debian:7
* el:6 (CentOS / RHEL 6.x)
* el:7 (CentOS / RHEL 7.x)
* sles:12
* sles:11

## Supported recipes

Visit <http://buildcurl.com>.

## Example

Want to get a precompiled ruby-2.3.0 for ubuntu:14.04, to be installed into `/usr/local`?

    curl buildcurl.com -LGfs --data-urlencode recipe=ruby --data-urlencode target=ubuntu:14.04 --data-urlencode version=2.3.0 --data-urlencode prefix=/usr/local | tar xzf - -C /usr/local

    /usr/local/bin/ruby -v
    #=> ruby 2.3.1p112 (2016-04-26 revision 54768) [x86_64-linux]

    /usr/local/bin/gem -v
    #=> 2.5.1

## Tips

### Display build log

The build log is streamed in the first response (which includes a `Location`
header to redirect to the resulting binary), so if you want to see it, just
make a first request without the follow redirect option, and then to the same
one with the `-L` flag:

    params="--data-urlencode recipe=ruby --data-urlencode target=ubuntu:14.04 --data-urlencode version=2.3.0 --data-urlencode prefix=/usr/local"
    curl buildcurl.com -fG $params && curl buildcurl.com -fGL $params -o result.tgz

More details at <https://github.com/crohr/buildcurl>.
