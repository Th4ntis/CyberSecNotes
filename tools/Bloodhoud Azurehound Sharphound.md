# About
BloodHound is a monolithic web application composed of an embedded React frontend with [Sigma.js](https://www.sigmajs.org/) and a [Go](https://go.dev/) based REST API backend. It is deployed with a [Postgresql](https://www.postgresql.org/) application database and a [Neo4j](https://neo4j.com/) graph database, and is fed by the [SharpHound](https://github.com/SpecterOps/SharpHound) and [AzureHound](https://github.com/SpecterOps/AzureHound) data collectors.

BloodHound uses graph theory to reveal the hidden and often unintended relationships within an Active Directory or Azure environment. Attackers can use BloodHound to quickly identify highly complex attack paths that would otherwise be impossible to find. Defenders can use BloodHound to identify and eliminate those same attack paths. Both red and blue teams can use BloodHound to better understand privileged relationships in an Active Directory or Azure environment.

## Links
[Bloodhoubd Github](https://github.com/SpecterOps/BloodHound)
[Bloodhound-CE Quickstart](https://bloodhound.specterops.io/get-started/quickstart/community-edition-quickstart)
[Sharphound Github](https://github.com/SpecterOps/SharpHound) - For AD Ingestion
[Azurehound Github](https://github.com/SpecterOps/AzureHound) - For EntraID and Azure Ingestion
[Bloodhound.py Github](https://github.com/dirkjanm/BloodHound.py) - For AD Ingestion
[Cypher Queries](https://queries.specterops.io/)

# Installing
## Kali
Purge older versions of neo4j and bloodhound
```
sudo apt purge -t neo4j bloodhound
```
![[Pasted image 20250909132151.png]]

Reinstall neo4j and bloodhound
```
sudo apt install -y neo4j bloodhound
```
![[Pasted image 20250909132156.png]]

First time running is
```
sudo bloodhound-setup
```
![[Pasted image 20250909132202.png]]

If you get this error:
```
sudo -u postgres psql
ALTER DATABASE postgres REFRESH COLLATION VERSION;
ALTER DATABASE template1 REFRESH COLLATION VERSION;
\q
```

Rerun:
```
sudo bloodhound-setup
```
![[Pasted image 20250909132208.png]]

This should open a wepbage to http://localhost:7474/browser for you to log in with neo4js default credentials: **neo4j:neo4j**. This info will also be shown when running the setup. You will need to:
Change the neo4j default password, and edit the `/etc/bhapi/bhapi.json` file with the updated password.
![[Pasted image 20250909132221.png]]
![[Pasted image 20250909132225.png]]
![[Pasted image 20250909132232.png]]

Now we can run bloodhound
![[Pasted image 20250909132239.png]]

This will open a webpage to http://127.0.0.1:8080
![[Pasted image 20250909132243.png]]

The default username and password is `admin`. Afterlogging in, it will want a new password.
![[Pasted image 20250909132248.png]]

# Usage
## Ingesting
Ingest files from [SharpHound](https://github.com/SpecterOps/SharpHound), [AzureHound](https://github.com/SpecterOps/AzureHound), or [Bloodhound-python](https://github.com/dirkjanm/BloodHound.py). They also have sample data you can use, for [Active Directory (AD)](https://raw.githubusercontent.com/SpecterOps/BloodHound-Docs/main/docs/assets/sample-data/ad_sampledata.zip) or [Azure](https://raw.githubusercontent.com/SpecterOps/BloodHound-Docs/main/docs/assets/sample-data/entra_sampledata.zip)

### Bloodhound-Python
```
bloodhound-python -u USER -p 'PASSWORD' -ns DNS-SERVER -d DOMAIN -c All
```

Then by going to http://127.0.0.1:8080/ui/administration/file-ingest - or Highlighting the Icon that looks like a User and a cog wheel on the left, and selecting `File Ingest`, then selecting `upload file(s)`
![[Pasted image 20250909132258.png]]
![[Pasted image 20250909132303.png]]
![[Pasted image 20250909132307.png]]

After uploading has completed, you will see it here. It may take a few minutes to ingest and look at all the data depending how much data you have. Wait until the status says complete
![[Pasted image 20250909132315.png]]

# Analyzing the data
On the left hand side, click the line graph icon and select explore, or go to http://127.0.0.1:8080/u/explore. From here is where we can look into any information needed.
![[Pasted image 20250909132319.png]]

For good base information, under `</> CYPHER` we can click the folder icon to see all their queries pre-loaded.
![[Pasted image 20250909132324.png]]

For example, `All Domain Admins`
![[Pasted image 20250909132332.png]]

## Queries
Tier Zero users with email
```
MATCH (n)
WHERE ((n:Tag_Tier_Zero) OR COALESCE(n.system_tags, '') CONTAINS 'admin_tier_0')
AND n.email <> ""
AND n.enabled = true
AND NOT toUpper(n.email) ENDS WITH ".ONMICROSOFT.COM"
AND NOT (
    (toUpper(n.email) STARTS WITH "HEALTHMAILBOX"
    OR toUpper(n.email) STARTS WITH "MSEXCHDISCOVERYMAILBOX"
    OR toUpper(n.email) STARTS WITH "MSEXCHDISCOVERY"
    OR toUpper(n.email) STARTS WITH "MSEXCHAPPROVAL"
    OR toUpper(n.email) STARTS WITH "FEDERATEDEMAIL"
    OR toUpper(n.email) STARTS WITH "SYSTEMMAILBOX"
    OR toUpper(n.email) STARTS WITH "MIGRATION.")
  AND
    (n.name STARTS WITH "SM_"
    OR n.name STARTS WITH "HEALTHMAILBOX")
)
RETURN n
```

AS-REP Roastable Tier Zero users (DontReqPreAuth)
```
MATCH (n:Base)
WHERE ((n:Tag_Tier_Zero) OR COALESCE(n.system_tags, '') CONTAINS 'admin_tier_0')
AND n.dontreqpreauth = true
RETURN n
```

Tier Zero computers not owned by Tier Zero
```
MATCH p=(n:Base)-[:Owns]->(:Computer)
WHERE NOT ((n:Tag_Tier_Zero) OR COALESCE(n.system_tags, '') CONTAINS 'admin_tier_0')
RETURN p
```

Tier Zero accounts that can be delegated
```
MATCH (m:Base)
WHERE ((m:Tag_Tier_Zero) OR COALESCE(m.system_tags, '') CONTAINS 'admin_tier_0')
AND m.enabled = true
AND m.sensitive = false
OPTIONAL MATCH (g:Group)<-[:MemberOf*1..]-(n:Base)
WHERE g.objectid ENDS WITH '-525'
WITH m, COLLECT(n) AS matchingNs
WHERE NONE(n IN matchingNs WHERE n.objectid = m.objectid)
RETURN m
```

Tier Zero AD principals synchronized with Entra ID
```
MATCH (ENTRA:AZBase)
MATCH (AD:Base)
WHERE ((AD:Tag_Tier_Zero) OR COALESCE(AD.system_tags, '') CONTAINS 'admin_tier_0')
AND ENTRA.onpremsyncenabled = true
AND ENTRA.onpremid = AD.objectid
RETURN ENTRA
// Replace 'RETURN ENTRA' with 'RETURN AD' to see the corresponding AD principals
LIMIT 100
```

Kerberoastable members of Tier Zero / High Value groups
```
MATCH (u:User)
WHERE (u:Tag_Tier_Zero) AND u.hasspn=true
AND u.enabled = true
AND NOT u.objectid ENDS WITH '-502'
AND NOT COALESCE(u.gmsa, false) = true
AND NOT COALESCE(u.msa, false) = true 
RETURN u
LIMIT 100
```

Enabled Tier Zero / High Value principals inactive for 60 days
```
WITH 60 as inactive_days
MATCH (n:Base)
WHERE ((n:Tag_Tier_Zero) OR COALESCE(n.system_tags, '') CONTAINS 'admin_tier_0')
AND n.enabled = true
AND n.lastlogontimestamp < (datetime().epochseconds - (inactive_days * 86400)) // Replicated value
AND n.lastlogon < (datetime().epochseconds - (inactive_days * 86400)) // Non-replicated value
AND n.whencreated < (datetime().epochseconds - (inactive_days * 86400)) // Exclude recently created principals
AND NOT n.name STARTS WITH 'AZUREADKERBEROS.' // Removes false positive, Azure KRBTGT
AND NOT n.objectid ENDS WITH '-500' // Removes false positive, built-in Administrator
AND NOT n.name STARTS WITH 'AZUREADSSOACC.' // Removes false positive, Entra Seamless SSO
RETURN n
```

Enabled users inactive for 180 days
```
WITH 180 as inactive_days
MATCH (n:User)
WHERE n.enabled = true
AND n.lastlogontimestamp < (datetime().epochseconds - (inactive_days * 86400)) // Replicated value
AND n.lastlogon < (datetime().epochseconds - (inactive_days * 86400)) // Non-replicated value
AND n.whencreated < (datetime().epochseconds - (inactive_days * 86400)) // Exclude recently created principals
AND NOT n.objectid ENDS WITH '-500' // Removes false positive, built-in Administrator
RETURN n
LIMIT 1000
```

## Stopping
### Linux
Top stop the bloodhound service, run:
```
sudo pkill bhapi
sudo pkill neo4j
```


