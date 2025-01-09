# Email/Username OSINT

Corporate usernames can be obnoxiously easy to guess and build. The standard of FIRSTNAME.LASTNAME@CORP.com is so common, it's ridiculous. Even more so when account management tools will simply take the first half of the email and reuse it as a username. We can use schemes like this to our advantage to search for a multitude of treasures like accounts on other services with the same username, credentials found in breaches, and associated sites or tools. When searching for usernames, you can uncover linked social media accounts and tons of relevant intelligence.

### Email Search Tools

* [MXToolBox](https://mxtoolbox.com/) - Collection of online tools that can gather multiple points of data surrounding an email address or domain
* [Seon.io](https://seon.io/intelligence-tool/#email-analysis-module) - Enrich user data based on a single email address
* [Epieos](https://tools.epieos.com/) - Enter an email address and see which sites the email address has been used.&#x20;
* [HoleHE](https://github.com/megadose/holehe) - CLI Tool to check if an email is attached to an account on sites like twitter, instagram, imgur and more than 120 others

### Email Discovery Tools

* [Hunter.io](https://hunter.io/) - Discover email addresses by company name
* [Phonebook.cz](https://phonebook.cz/) - Phonebook lists all domains, email addresses, or URLs for the given input domain.
* [Voilanorbert](https://www.voilanorbert.com/) - Discover email addresses by company name
* [Connect.Clearbit](https://connect.clearbit.com/) - Email discovery tool, only works in chrome.
* [Email Format ](https://www.email-format.com/)- Find the email address format for a given company or domain.
* [Snov.io](https://snov.io/email-finder) - Locate employee email addresses via domain name.
* [TheHarvester](https://github.com/laramies/theharvester) - This tool is the defacto standard for email intelligence gathering. It checks a large array of sources to pull together information. It can leverage APIs of other services such as Spyse or Shodan to improve the search. Remember these will require an API key to use. I have found that between the above html tools and this, it will satisfy your email searching needs.
* [Email Hippo](https://tools.verifyemailaddress.io/)
* [Email Checker](https://email-checker.net/validate)

### Tools

* [breach-parse](https://github.com/hmaverickadams/breach-parse)

```
breach-parse 
```

[Breached password list from Magnet link](https://magnet/?xt=urn:btih:7ffbcd8cee06aba2ce6561688cf68ce2addca0a3\&dn=BreachCompilation\&tr=udp%3A%2F%2Ftracker.openbittorrent.com%3A80\&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969\&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969\&tr=udp%3A%2F%2Fglotorrents.pw%3A6969\&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337)

* [theHarvester](https://github.com/laramies/theHarvester)

```
theHarvester -d domain -b search
```

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

[h8mail](https://github.com/khast3x/h8mail)

```
h8mail -t target@domain.com
```

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Username Search Tools

* [WhatsMyName](https://whatsmyname.app/) - This tool allows you to enumerate usernames across many different websites.
  * [WhatsMyName Github](https://github.com/WebBreacher/WhatsMyName)
* [UserSearch](https://usersearch.org/index.php) - Search Engine for Usernames
* [Name Check](https://namechk.com/) - See if a username is available across multiple platforms
* [NameCheckup](https://namecheckup.com/)
* [Sherlock](https://github.com/sherlock-project/sherlock) - Hunt down social media accounts by username across social networks
* [SocialCcan](https://github.com/iojw/socialscan) - Python library and CLI for accurately querying username and email usage on online platforms
* [AnalyzeID](https://analyzeid.com/username/) - Social media username checker. Gather information on the taken username and get a summary of who the person is
* [IDCrawl](https://www.idcrawl.com/) - A free people search engine that organizes social network information, deep web information, phone numbers, email addresses and more

### Tools

* [whatsmyname](https://github.com/WebBreacher/WhatsMyName)
* [sherlock](https://github.com/sherlock-project/sherlock)

```
sherlock user
```

<figure><img src="../.gitbook/assets/image (4) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
