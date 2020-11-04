---
layout: page
title: "About Me"
permalink: /about/
---

## Agile Full-Stack Developer

Experienced software engineer specializing in integrating open-source components into end-to-end solutions.
T-Shaped agile team member versatile in switching between engineering, design, development, test, deployment and support roles.
Mission-driven to find creative solutions with the enthusiasm and dedication to see them through to completion.

## WORK EXPERIENCE (AT&T 1987-2020)

### Lead Dragon Software Engineer, Principal Member of Technical Staff
2012 - Jul 2020 

Dragon is AT&T's Domain Name Service (DNS) provisioning system for centralized management of DNS zone data serving multiple DNS server complexes.  AT&T Mobility Universal Services Platform (USP) is an IP multimedia service that handles all voice/video over LTE for the 4G/5G wireless network.  

* Worked in a multi-functional team of network engineers, testers and operators to architect, design, develop, test and support USP on the Dragon platform.  
* Architected a high-performance DBOR spreadsheet to CSV converter using Docker, Python/Pandas.  Now 10x faster than Perl.  
* Designed a RESTful interface and implemented the server using Perl, Moose, DBI, DBD::Informix, Plack, Starman to shape traffic with DNS SRV record parameters.  Used a TDD approach, and delivered functionality with 3500 lines of Perl.  
* Authored ~7000 lines of Perl/ksh of the AT&T Mobility Extract-Transform-Load (ETL) tools to use Perl threads in a work-queue, worker pool model, increasing performance by 5x.  
* Wrote the Cache Flush Tool, a web application to flush bad records from DNS caching resolvers.  2500 lines of Perl, CGI, Apache, Javascript, AJAX.  
* Architected and developed a pull model (~3500 lines of client/server Perl) to package the latest snapshot of DNS server configurations and initiate pulls from the Dragon server.  

### Zen Software Engineer, Principal Member of Technical Staff
Feb 2020 - Jul 2020 

Zen is a Kafka and InfluxDB based data collector for AT&T's Edge Cloud.

* Designed a framework for GitOps provisioning of VMs by function.  
* Wrote an integrated Ansible script to install platform and application software on a heterogeneous cluster of Edge Cloud VMs.  

### Lead DNS-C Software Engineer, Principal Member of Technical Staff
2016 - 2018 

DNS-C (DNS-Controller) was designed as the central system for the management of AT&T Mobility’s DNS data implemented on a modern Linux/Oracle platform.  

* Architected the Mobility OAM/VitalQIP IP Address Management (IPAM) to DNS-C interface, wrote the daemon to convert hourly full database dumps into a set of differences to apply to the DNS-C database.  Delivered as 3500 lines of Perl, ran perfectly in production for years!  
* Wrote the migration processing tools in 5000 lines of Perl for parsers for ISC bind zone files to convert other AT&T Mobility data into the canonical format, where they could be compared to the database contents and differences applied iteratively to the database.  
* Designed a batch processing data format and wrote a multi-threaded utility to load data via REST into Oracle.  Used Perl threads and a worker pool/work queue model to parallelize migration of 5000 zones.  

### Lead RTTP Software Engineer, Principal Member of Technical Staff
2008 - 2012 

RealTime Transaction Platform (AT&T U-verse TV).  

* Wrote the RTTP data-mart, a Java/JDBC/Mysql caching layer between back-end LDAP and SOAP Web Service servers.  The data-mart is an object-oriented class hierarchy capable of finding needed data efficiently from a pool of data-replicated servers.  
* Configured Mysql with circular primary-primary replication, engineered for 4 geo-redundant sites, and primary-replica replication within each site for reliability and read scalability.  
* Wrote a X509 client certificate enrollment proxy for AT&T U-verse (TV) and AT&T Digital Life (home security) so that devices like set top boxes and IoT sensors can acquire/renew their certificates.  Used an Java/Artix JAX-RPC/JAX-WS web service for the client interface and a Perl daemon process to interface between the database and certificate server.  
* Using Java and mysql, designed a well-factored set of cache tables and wrote the SOAP client to get per-subscriber channel lineup data and store non-redundantly in the data-mart.  Used an Artix JAX-RPC/JAX-WS front-end.  

### WorldNet Software Engineer, Principal Member of Technical Staff
2005 - 2008 

WorldNet (AT&T dial-up, Comcast, Insight, Mediacom high speed internet).

* Maintained WebMail interface to OpenLDAP AddressBook.  
* Modified OpenLDAP to support multiple embedded Perl interpreters for near linear scalability.  

### WorldNet Netnews Administrator, Principal Member of Technical Staff
2000 - 2010 

WorldNet (AT&T dial-up, Comcast, Insight, Mediacom high speed internet). 

* Maintained netnews complex of Highwinds software.  
* Provided NNTP to POP3 authentication module.  
* Modified stunnel to implement bandwidth limits for "bring-your-own-internet" customers.  

### WorldNet Account Registration Developer, Member of Technical Staff
1996 - 2000

WorldNet was AT&T’s dial-up internet service.  

* Used Apache CGI, Perl, DBI/DBD::Oracle, Oracle PL/SQL to implement the account registration and provisioning process.  
* Automatic Account Restore feature saved $50/care phone call thousands of times a day.  

### PersonalLink Techtools, Member of Technical Staff
1995 - 1996 

Member of the TechTools team supporting AT&T’s dial-up service for the Sony Magic Link.  

* Wrote a suite of version control/software configuration management tools in ksh/Perl. 

### SubNetwork-2000 Software Engineer, Member of Technical Staff
1993 - 1995 

Lead developer for SNC-2000, a GUI for managing a network of digital multiplexers.  

* Object-oriented design, implemented in C++.  

### Operations Systems Prototyper, Member of Technical Staff
1990 - 1993 

Prototyper, OS Evolution Lab, hosted demonstrations of AT&T Operations Systems.  

* Prototyped GUIs in AT&T Display Construction Set.  

### EADAS Systems Engineer, Member of Technical Staff
1987 - 1990 

Systems Engineer for the Engineering and Administrative Data Acquisition System.  

* Gathered RBOC and NTT customer requirements and wrote requirements documents.  

## PASSION PROJECTS

### Picture Tagger
2020

Digital camera family picture tagger using Docker, Python, and Flask for the REST server and a Typescript, Angular GUI REST client.  Users can review pictures on their web browser by date range and persistently tag for later group retrieval by tag.

### Whole House DVR
2010-2020

A TIVO-like DVR software collection, including scraping daily listings per OTA channel from IMDB.com, prioritizing recording to 2 to 4 tuners, recording daemons, transcoding daemons, viewing server and garbage collection daemon for deleted recordings.  Included modifying hdhomerun software to slice captured transport stream files into 5-minute segments for later batch transcoding with ffmpeg.  Uses mplayer command pipeline to play segments seamlessly in the correct order. Used Perl, Apache, CGI, Javascript, AJAX interface for viewing upcoming recordings and channel guide.

### NY Mets Radio DVR
2014-2017

Because baseball is slow, wrote radio capture software to record audio from a tuned radio to WAV files and transcode to MP3.  Also wrote a web service to combine all un-heard audio segments on the fly for naive players, with the session data awareness to avoid including redundant segments.  As an additional feature, acquired game start times daily from the web, and recorded until the game was marked as final on MLB.com (for extra innings and rainouts).  Used Javascript, JQuery, AJAX, Perl, Apache, CGI.  Almost makes baseball enjoyable!

### Holmdel Softball Club Webmaster
1997-2020

Generate league schedules yearly, track game status from score reports on the web server daily.  Wrote a script to generate league standings and team (re)schedules on each update and push to the web site.

### Netnews Multipart Binary Downloader
2010-2016

Wrote a netnews daily header parser to download headers from selected newsgroups and identify multi-part binaries.  This output was used as a database to match against patterns of missed TV episodes (from the Whole House DVR) caused by power outages.

## EDUCATION

**Masters of Science (Sc.M.) Computer Science,** Brown University, Providence, RI  
Member of the Computer Graphics Group, specialized in Non-Uniform Rational B-Spline curves and surfaces for 3-D modelling and ray-tracing.  
<br>
**Bachelor of Arts (B.A.) in  Mathematics,** Hamilton College, Clinton, NY  
Graduated Summa Cum Laude. Senior research into automated programming for novice programmers.  

## Online Courses
AWS: Pursuing certification as AWS Solutions Architect at the Associate level.

* "AWS Cloud Practitioner Essentials (Second Edition)"
* "AWS Certified Solutions Architect - Associate (SAA-C02)"

Azure: Planning to get a Azure Fundamentals certificate.

* "Microsoft Azure Fundamentals" 
* "Exam Prep: MS Azure Fundamentals(AZ-900)" 

