# leighsmithcapital.com

Static site. No build step, no JavaScript, no dependencies.

```
index.html        Overview
the-firm/         The Firm
style.css         shared stylesheet
seal.svg          favicon and monogram
CNAME             the custom domain, read by GitHub Pages
```

Everything lives at the repo root because GitHub Pages serves a branch from
root or `/docs` only, never from a subfolder.

## Design

Libre Caslon Display and Libre Caslon Text throughout, one family in two
optical sizes. Bottle green `#1D3327` against a cool laid paper `#ECEDE6`,
with an antique brass hairline `#A98B4E` used only against the green: on paper
it computes to 2.75:1 and washes out.

Two ornaments and no others, the engraved monogram seal and the swelled rule
(the tapered letterpress diamond). No cards, no shadows, no shaded panels, no
photography, and no navigation beyond two words.

The copy states nothing that has not been confirmed. No personal names, no
address, no phone, no holdings, no founding date, no team. The one figure on
the site is the AUM line on the Overview page.

## Local preview

```
python3 -m http.server 4321
```

## Deploy

Push to `main`. GitHub Pages serves it.

## DNS

Nameservers stay at GoDaddy. **Live Microsoft 365 mail runs on this domain**,
so the MX record, the SPF TXT record and any autodiscover record must not be
touched. Only the four apex A records belong to the website.

| Host | Type | Value |
|---|---|---|
| `@` | A | `185.199.108.153` |
| `@` | A | `185.199.109.153` |
| `@` | A | `185.199.110.153` |
| `@` | A | `185.199.111.153` |

`www` stays a CNAME to the apex. The documented setup points it at the Pages
host instead, but that would publish the owning account's username in DNS for
anyone who ran a lookup. Pointing it at the apex lands on the same servers and
reveals nothing.

### If the apex A records will not edit

GoDaddy greys out the edit and delete controls on the apex A records and says
*"You can't modify records that have been applied by a product or service
connected to your domain."* That is domain forwarding, not a permissions
problem. This domain had a forwarding rule sending `leighsmithcapital.com` to
`https://leighsmithcapital.com`, a 302 to itself, which owned the two parked A
records.

Delete the rule under **DNS > Forwarding** and the parked A records collapse
into one editable row. Forwarding is web only, so removing it cannot affect
mail.

The record-type dropdown in the **Add New Record** form does not respond to
synthetic clicks; it has to be set as a form value. The Copy button on a record
row copies the value to the clipboard, it does not duplicate the row. Use
**Add another value** on a single A record to attach all four IPs at once.
