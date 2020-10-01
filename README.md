# langnull
Guide to filter out subdomains that contain language and country codes of ISO-639-1, ISO-639-2 &amp; ISO-3166.

## Usage
1. Simply download the `language_country_codes.txt` file or use a `wget` on the raw file.
2. Lastly, use it on a subdomain list:

`$ cat subdomains.txt | grep -v -f language_country_codes.txt`

### Optional
You could also add a function in your bash profile.
I simply added a couple lines in my ~/.profile

```
langnull(){
  grep -v -f /path/to/language_country_codes.txt
}
```

## Info
The `language_country_codes.txt` file contains two unique patterns which use `//{countryCode}-` and `//{countryCode}.`
They were specifically meant for http-checked subdomains and they will remove any line in a subdomains file if there's a country code between `http(s)://{here}.blabla.com` or
`http(s)://{here}-dev.blabla.com`.

By that being said, you don't have to worry what comes after the `http(s)://` since I already added pretty much every single logical combination there could be, but you can always add more. 😊

### Example Usage:
`$ cat subdomains-probe.txt | langnull`

- Output:
```
https://itworks.hoohaa.com
```

`$ cat subdomains-probe.txt`

- Output:
```
https://itworks.tw.hoohaa.com
https://itworks.eu.hoohaa.com
https://eu.itworks.hoohaa.com
https://eu-itworks.hoohaa.com
https://itworks-eu.hoohaa.com
https://itworks.hoohaa.com
```
