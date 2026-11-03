# trancendance.net – DNS backup

Captured 2026-11-03 via Google Public DNS (dns.google), before any changes for the GitHub Pages move.
These are the publicly visible records. The authoritative zone at Netfirms may hold entries that
don't resolve publicly (for example records with no public answer), so this is a snapshot of what
the internet sees, not an export of the Netfirms control panel.

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

## For the GitHub Pages cut-over
Change only the web records; leave NS, MX, mx.* A records and TXT untouched so mail keeps working.

- Delete: A trancendance.net → 107.170.207.9
- Delete or leave: wildcard A → 107.170.207.9 (GitHub Pages ignores it; delete if the droplet is retired)
- Add: A trancendance.net → 185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153
- Change: CNAME www → djsmileymike.github.io.

Note for later: because the old site lives on a DigitalOcean droplet at 107.170.207.9, retrieving
the archive (files + database) means logging into DigitalOcean, not Netfirms. Check for a
DigitalOcean account/billing email under that domain.
