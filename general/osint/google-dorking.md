# Google Dorking

## Google and Google Dorking

We all know google is a search engine that collects and indexes various websites from all over the internet, but some don't know how powerful it really is. Google hacking, also named Google dorking, is a technique that uses Google Search and other Google applications to find security holes in the configuration and computer code that websites are using.

### What is Dorking

**Dorking** is basically an advanced search where we use operators that function as a filter to direct the search directly to where we want. We also use symbols to search for exact words or phrases. This will help us to search almost any search engine that we find on the internet. This involves making use of search engines to their complete potential to uncover outcomes that are not noticeable with a routine search. It enables us to refine out searches and dive deeper, and with better accuracy, right into web pages as well as files that are available online. Revealing covert documents and safety and security defects by dorking does not require a good deal of technical knowledge. It actually comes down to discovering just a few search strategies and using them across a variety of online search engine.

### Why we need google dorks

Everyone can use google dorks for a different purpose. Some of the most common reasons for using google dorks:

* Cyber Security roles use google dorks to find critical information that can be exposed by mistake, or by someone knowingly, about anything so that they can later on hide or delete that so that no one can use that for any wrong purpose.
* Researchers, content writers, journalists, etc use google dorks to gather all the information available on google about a particular topic so that they can use that information for reaching their own goals.
* Students use google dorks to find answers to their questions which are from their textbook or asked by someone or for finding leaked versions of a course or a book for free.
* Companies and their employees use google dorks to gather information about their competitors and for finding honest reviews of their products or services so that they can use that information further for improving their products and services and which in results helps their company grow faster.

### What can we find from Google Dorks

Google dorks can be used to find a variety of information in many aspects, but it's mainly used to find the information on:

* Critical information of a website, company, organization, software, etc.
* Blogs, articles, research papers, etc on a particular topic
* Leaked documents, courses, eBooks, etc
* Reviews about a company, it's products and services
* Finding solutions of answers of textbook questions

There are many other kinds of information which can be found via google dorks very easily.

### Using Google Dorks

|                  Dork                  |                                                         Used for                                                        |                  Example                 |
| :------------------------------------: | :---------------------------------------------------------------------------------------------------------------------: | :--------------------------------------: |
|    "specified\_phrase or statement"    |                               Shows only those pages that contains exact word or statement                              |           "Is hacking illegal"           |
|                  site:                 |                         Removes search results from all other websites except the specified one                         |          site:github.com th4ntis         |
|         inurl:specified\_phrase        |                              Shows search results which contains the specified word in url                              |           inurl:ethical hacking          |
|            inurl:word1 word2           |                              Shows search results that contain either of the words, or both                             |         inurl:hacking programming        |
|          allinurl:word1 word2          |                            Shows the search results that contain both of the specified words                            |       allinurl:hacking programming       |
|           intitle:word1 word2          | Shows those search results that mention the word in their title and mention the specified word anywhere in the document |        intitle:hacking networking        |
|                 cache:                 |                               Shows a cached version of the website if the website is down                              |             cache:netflix.com            |
|              intext:word1              |                     Shows only those pages containing that specific word(s) somewhere in the context                    |            intext:bug hunting            |
|          allintext:word1 word2         |                         Only shows pages containing the specified words somewhere in the context                        |       allintext:hacking networking       |
|           intitle:”index of”           |                                                  Shows open ftp servers                                                 |    intitle:”index of spiderman movie”    |
|         inurl:view/index.shtml         |                                    Shows live cameras that don’t have any protection                                    |          inurl:view/index.shtml          |
| filetype:pdf/doc/ppt specified\_phrase |             Shows only pages that contains the document of that type and contains specific word in file name            |       filetype:pdf ethical hacking       |
|                   +                    |                                     Shows pages that must contain the specified word                                    | <p>ethical hacking + free course<br></p> |
|                    -                   |                                        Removes results that contain certain words                                       |       ethical hacking - paid course      |
|                  feed:                 |                                       Shows specified RSS feed for specified work                                       |               reed:hacking               |
|                   ip:                  |                                         Finds websites organized by specified IP                                        |             ip:_54.239.28.85_            |

We can use googles [normal search](https://www.google.com/) as well as their [Advanced Search page](https://www.google.com/advanced\_search).

Of course we can combine these searches as well.

We can also use BOOLEAN searches in Google by using AND / OR

`google dorking filetype:pdf OR filetype:doc OR filetype:docx`

Learning resource: [TryHackMe - Google Dorking Room](https://tryhackme.com/room/googledorking)
