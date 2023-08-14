# DDNS Cloudflare Bash Script for OpenWRT

## Requirements

- curl
- bash
- Cloudflare [api-token](https://dash.cloudflare.com/profile/api-tokens) with ZONE-DNS-EDIT Permissions
- DNS Record must be pre created (api-token should only edit dns records)

### Creating Cloudflare API Token

To create a CloudFlare API token for your DNS zone go to [https://dash.cloudflare.com/profile/api-tokens][cloudflare-api-token-url] and follow these steps:

1. Click Create Token
2. Select Create Custom Token
3. Provide the token a name, for example, `example.com-dns-zone-readonly`
4. Grant the token the following permissions:
   - Zone - DNS - Edit
5. Set the zone resources to:
   - Include - Specific Zone - `example.com`
6. Complete the wizard and use the generated token at the `CLOUDFLARE_API_TOKEN` variable for the container

## Config file

You can use default config file _update-cloudflare-dns.conf_ or pass your own config file as parameter to script.

Place the **config** file in the directory as the **update-cloudflare-dns**

## Config Parameters

| **Option**                | **Example**      | **Description**                                                                                                           |
| ------------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------- |
| dns_record                | ddns.example.com | DNS **A** record which will be updated, you can pass multiple **A** records separated by comma                            |
| cloudflare_zone_api_token | ChangeMe         | Cloudflare API Token **KEEP IT PRIVATE!!!!**                                                                              |
| zoneid                    | ChangeMe         | Cloudflare's [Zone ID](https://developers.cloudflare.com/fundamentals/get-started/basic-tasks/find-account-and-zone-ids/) |
| proxied                   | false            | Use Cloudflare proxy on dns record true/false                                                                             |
| ttl                       | 120              | 60-7200 in seconds or 1 for Auto                                                                                         |


## Running The Script

When placed in _/usr/local/bin/_

```shell
update-cloudflare-dns
```

With your config file (need to be placed in same folder)

```shell
update-cloudflare-dns yoru_config.conf
```

Or manually

```shell
<path>/.update-cloudflare-dns.sh
```

## Automation With Crontab

You can run the script via crontab

```shell
crontab -e
```

### Examples

Run every minute

```shell
* * * * * /usr/local/bin/update-cloudflare-dns
```

Run with your specific config file

```shell
* * * * * /usr/local/bin/update-cloudflare-dns myconfig.conf
```

Run every 2 minutes

```shell
*/2 * * * * /usr/local/bin/update-cloudflare-dns
```

Run at boot

```shell
@reboot /usr/local/bin/update-cloudflare-dns
```

Run 1 minute after boot

```shell
@reboot sleep 60 && /usr/local/bin/update-cloudflare-dns
```

Run at 08:00

```shell
0 8 * * * /usr/local/bin/update-cloudflare-dns
```

## Logs

This Script will create a log file with **only** the last run information
Log file will be located at the script's location.

Example:

```bash
/usr/local/bin/update-cloudflare-dns.log
```

## Limitations

- Does not support IPv6

## License

### MIT License

Copyright© 3os.org @2020

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to
deal in the Software without restriction, including without limitation the
rights to use, copy, modify, merge, publish, distribute, sublicense, and/or
sell copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NON-INFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS
IN THE SOFTWARE.

<!-- urls -->
<!-- appendices -->

[cloudflare-api-token-url]: https://dash.cloudflare.com/profile/api-tokens 'Cloudflare API Token'

<!-- end appendices -->
