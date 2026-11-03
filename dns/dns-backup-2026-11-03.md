# trancendance.net – DNS backup

Captured 2026-11-03, before any changes for the GitHub Pages move.

## Authoritative zone (Netfirms control panel)

Transcribed from the Netfirms "DNS & Nameservers → DNS Records" page on 2026-11-03
(screenshot: `netfirms-dns-records-2026-11-03.png`). Panel says last updated 03/23/2021 12:22:36 AM.
Two values are truncated in the panel UI and were completed from public lookups where possible.

| Record | Name | Content | Priority | Last updated |
|---|---|---|---|---|
| A | @ | 107.170.207.9 | 0 | 04/16/2017 6:55:52 PM |
| A | ftp | 107.170.207.9 | 0 | 04/16/2017 6:55:52 PM |
| A | mx | 66.96.140.128 | n/a | 01/14/2017 9:54:29 PM |
| A | mx | 66.96.140.129 | n/a | 01/14/2017 9:54:29 PM |
| A | popmail | 66.96.160.145 | n/a | 01/14/2017 9:54:29 PM |
| A | pop | 66.96.160.145 | n/a | 01/14/2017 9:54:29 PM |
| A | imap | 66.96.160.145 | n/a | 01/14/2017 9:54:29 PM |
| A | smtp | 66.96.160.145 | n/a | 01/14/2017 9:54:29 PM |
| A | mail | 66.96.160.145 | n/a | 01/14/2017 9:54:29 PM |
| A | webmail | 66.96.160.48 | n/a | 01/14/2017 9:54:29 PM |
| A | email | 66.96.160.48 | n/a | 01/14/2017 9:54:29 PM |
| A | * | 107.170.207.9 | 0 | 04/16/2017 6:55:52 PM |
| CNAME | www | trancendance.net | n/a | 01/14/2017 10:11:03 PM |
| CNAME | dkim._dom… (truncated; almost certainly `dkim._domainkey`) | cur.dkim.v.eigmail.… (truncated; Endurance/Netfirms DKIM host) | n/a | 04/27/2017 3:24:04 … |
| MX | @ | mx.trancendance.net | 30 | 01/14/2017 9:54:29 PM |
| MX | * | mx.trancendance.net | 30 | 01/14/2017 9:54:29 PM |
| NS | @ | ns1.netfirms.com | n/a | 01/14/2017 9:54:29 PM |
| NS | @ | ns2.netfirms.com | n/a | 01/14/2017 9:54:29 PM |
| SOA | @ | ns1.netfirms.com. hostmaster.netfirms.com. 2017011495 10800 3600 604800 3600 | n/a | 01/14/2017 9:54:29 PM |
| TXT | @ | v=spf1 ip4:66.96.128.0/18 include:_spf.google.com ?all | n/a | 03/23/2021 12:22:36 … |
| TXT | @ | google-site-verification=U0BGsu9SIUgaEfxTwY-aERcn65c_s6eyOTzhAhtngio | n/a | 03/23/2021 12:15:08 … |

Records the public lookups below did not see: ftp, popmail/pop/imap/smtp/mail, webmail/email, the
wildcard MX, and the DKIM CNAME. All of the mail-related ones point at Endurance/Netfirms ranges
(66.96.x.x). To capture the two truncated DKIM values exactly, open that row's menu (⋮ → Edit) in the
Netfirms panel and copy the full Name and Content.

## Public view (Google Public DNS, dns.google)

What the internet sees, as a cross-check on the panel above.

## Nameservers / zone
| Type | Name | TTL | Data |
|---|---|---|---|
| NS | trancendance.net. | 3600 | ns1.netfirms.com. |
| NS | trancendance.net. | 3600 | ns2.netfirms.com. |
| SOA | trancendance.net. | 3600 | ns1.netfirms.com. hostmaster.netfirms.com. 2017011495 10800 3600 604800 3600 |

Zone serial 2017011495 suggests the zone was last edited around January 2017.

## Web
| Type | Name | TTL | Data |
|---|---|---|---|
| A | trancendance.net. | 3600 | 107.170.207.9 |
| CNAME | www.trancendance.net. | 3600 | trancendance.net. |
| A | *.trancendance.net. (wildcard) | 3600 | 107.170.207.9 |
| AAAA | trancendance.net. | – | none |

The wildcard was confirmed by resolving a random subdomain (and dev.trancendance.net) to the same IP.
107.170.207.9 is a DigitalOcean address, so the WordPress site is on a DigitalOcean droplet, not on
Netfirms shared hosting. Netfirms is the registrar/DNS host only.

## Mail
| Type | Name | TTL | Data |
|---|---|---|---|
| MX | trancendance.net. | 3600 | 30 mx.trancendance.net. |
| A | mx.trancendance.net. | 3600 | 66.96.140.128 |
| A | mx.trancendance.net. | 3600 | 66.96.140.129 |
| TXT | trancendance.net. | 3600 | v=spf1 ip4:66.96.128.0/18 include:_spf.google.com ?all |

66.96.128.0/18 is the Endurance / Netfirms mail range, so any @trancendance.net mail is handled by
Netfirms mail servers (with an SPF allowance for Google as a sender). No DMARC or DKIM records found.

## Verification
| Type | Name | TTL | Data |
|---|---|---|---|
| TXT | trancendance.net. | 3600 | google-site-verification=U0BGsu9SIUgaEfxTwY-aERcn65c_s6eyOTzhAhtngio |

## For the GitHub Pages cut-over (Netfirms panel edits)

Touch only the rows listed here. Every mail row (mx, popmail, pop, imap, smtp, mail, webmail, email,
both MX rows, the DKIM CNAME, the SPF TXT) and the NS/SOA rows stay exactly as they are.

1. **A @ 107.170.207.9** → edit the Content to `185.199.108.153`
2. **Add** A @ `185.199.109.153`
3. **Add** A @ `185.199.110.153`
4. **Add** A @ `185.199.111.153`
5. **CNAME www trancendance.net** → edit the Content to `djsmileymike.github.io`
6. **A \* 107.170.207.9** (wildcard) → delete, or leave until the DigitalOcean droplet is retired. GitHub ignores it either way.
7. **A ftp 107.170.207.9** → leave; harmless, only matters if the droplet goes away.

Then in GitHub: repo Settings → Pages → Custom domain → `trancendance.net` → Save. Wait for the DNS
check to pass (Netfirms says 4–8 hours to propagate; usually faster), then tick **Enforce HTTPS**.
GitHub will serve both trancendance.net and www.trancendance.net and redirect the github.io URL to the domain.

Note for later: because the old site lives on a DigitalOcean droplet at 107.170.207.9, retrieving
the archive (files + database) means logging into DigitalOcean, not Netfirms. Check for a
DigitalOcean account/billing email under that domain.
