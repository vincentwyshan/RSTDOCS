======================
Planning For 2016 Q3
======================


.. Note::

    - Please follow the contents menu reading this document.
    - Some background introduction in this document, but `Milestones`_ is the 
      actual planning to follow up.


.. Contents::
    :depth: 3


Shanghai and Hangzhou office startup
=====================================
We should make our Shanghai and Hangzhou office come into operation in september
1st.

Setting up office
------------------

Jianwei.Zhu is working on this. He has a more detailed planning. Below are the
brief primary objectives.

#. Office decoration
#. Desk, chairs, etc.
#. Anything else


Network, computers
----------------------
Hawking.Wan is working on this, He has a more detailed planning about the network,
also he will work together with US colegues.

#. Purchasing computers
#. VPN, employee accounts, etc.


Recruitment
------------

Our recruitment targets are:

#. HT conversion, to take over(or partly) MarketSmith, wogutan, Panary
#. iOS/Android, to take over MarketSmith HK
#. Database/financial developer, to start building the US/HK/A stock database
#. Others: including designer, .net programer, sql developer, BSA, English translators, content editors

**Recently recruiting** (below listed are those people I have contacted):

===============    ================    ====================================
Technology          Name                Objective
===============    ================    ====================================
.NET/database      Zuojia.Sheng(HT)    MarketSmith
.NET/database      Qijing.Zhang(HT)    MarketSmith
.NET/database      Qingqing.Zheng      MarketSmith
QA                 Wei.Chen(HT)        Testing Development
BSA/QA             Huan.Liu(HT)        BSA/MarketSmith
BSA/QA             Yu.Liu(HT)          BSA/Panary
IT/DBA             Jerry(YuHui)(HT)    IT/DBA          
iOS/Android        Xin.Chen            MarketSmith HK
Database           Xin.Guan            Data development
Database           Zehua.Wei           Data development
===============    ================    ====================================


Data development
=================

We will build US, IBD News, HK, A-stock databases for both commercial usage(selling database)
and product development(support Panary, MarketSmith).

We will create a streaming data distribution service, there is an opportunity to sell 
realtime streaming data feed.


US market and fundamental data(USDB)
-------------------------------------

Brief introduction:
~~~~~~~~~~~~~~~~~~~~~~

#. Start from WONDB
#. Including:
    #. US market database
    #. US fundamental database
    #. Also US historical price(quotes) database
#. Rich documentation
#. Localization needs, we should translate some English literal data to chinese


How to create USDB:
~~~~~~~~~~~~~~~~~~~~~~

#. Create a testing WONDB environment for the USDB project
#. Gather all the documents and informations about WONDB, to understand the 
   WONDB structure and WONDB data indicators
#. Write an USDB sturcture documentation, which describe all the logic about 
   tables/fields/unique keys/comments
#. Based on the full USDB documentation, start developing the data generating
   scripts
#. Deployment, testing (create a task manage system to deploy/manage the 
   generating tasks)


How to publish USDB:
~~~~~~~~~~~~~~~~~~~~~~
We should have a database publish tool(or system), which is in charge of 
publishing and delivering data to our clients(or development projects). 

This publish tool should be able to do:
    #. Have a publish server, and a client to receive data from publish server
    #. Transfer data to primary databases, including SQL Server, Oracle, MySQL
    #. Permission control


How many indicators in USDB:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We will have a full independent document to describe USDB indicators. 

======================= =====================
Indicator Category      Description
======================= =====================
Equities
Company
Shareholder
Financial statement
Dividends
etc..
======================= =====================



US realtime streaming quotes(USQUOTE)
-------------------------------

Hawking.Wan will make a detailed plan for this part.

**The objectives:**

- IT/network architecture
    #. network from WON US server to Nasdaq 
    #. network between WON US and WON China (Aliyun?)
- Researching Nasdaq streaming data feed
    #. Learn the Nasdaq streaming protocol and data format
    #. Do we need to convert the Nasdaq data format to particular format(our 
       format or client's format)
- Design and implement streaming data distribution service software
    #. We should have a distribution service to distribute the streaming quotes
       data
    #. Authorization is the necessary feature


IBD news localization
----------------------

We think it's worth to translate IBD news to Chinese, we may have some clients
need those news materials in Chinese.

What's the product form
~~~~~~~~~~~~~~~~~~~~~~~~

- All the news must contain the declaration which declare that news from IBD
- We may directly sell a database which has the all IBD news
- We may have news feed, client get our news by fetching the news feed

How to processing IBD news(localization)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- A database to store IBD news
    + Grab all English version IBD news, fetching from IBD database directly or 
      fetching from news feed
    + Design data tables for Chinese version IBD news 
- Using an editing UI to translate IBD news
    + Reading and picking English IBD news
    + Translating, Editing
    + Version control, permission control
    + Publish workflow
- A distribution service(system)


A-stock database(CNDB)
-----------------------

Brief introduction
~~~~~~~~~~~~~~~~~~~~~
Listed are primary A-stock data categories:
    #. IPO
    #. Shareholders
    #. Financial statements
    #. etc.


Vendor choices
~~~~~~~~~~~~~~~~~
#. GilData (聚源)
#. CnInfo (巨潮)
#. Gaotimes (港澳)
#. Wind (万得)
#. 贝格资讯

How to create CNDB database
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Convert vendor's database to our database:
    - Design our database structure based on vendor's database structure
    - Convert one or multiple verdors's database to our database

How to use CNDB database
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For panary and marketsmith:
    + Choice 1, we can create datafeed api to fulfill the specific data format
      in WONDB
    + Choice 2, we can `publish our CNDB database <#how-to-publish-usdb>`_ to WONDB team

For other application scenarios:
    + publish/subscribe our CNDB database


HK-stock database(HKDB)
------------------------

We already have a HKDB structure and indicators design material, it's better we see what Hongkong 
market data we have and decide how many data we should buy.

Vendor choices
~~~~~~~~~~~~~~~~
#. CnInfo (巨潮)
#. TEJ
#. Etnet

The create and publish process just like CNDB.


HK Realtime quotes(HKQUOTE)
----------------------------

Vendor Choices
~~~~~~~~~~~~~~~
#. Does WON already have a HKQUOTE vendor?
#. Etnet

The create and publish process just like USQUOTE. And the differences are:
    - Design the network architecture based on datasource(Which vendor we will choose)
    - Learn the streaming data document, it might be different document for different
      vendor


wogutan.com
============

Questions
----------

MarketSmith HK and wogutan.com both have a chinese language website, we may think about
position of the 2 products. A few topics we need considering like:
    - What's the target customer difference between wogutan.com and MarketSmithHK
    - We have plan to localize IBD news, where should we publish the chinese version 
      IBD news to.
    - wogutan means "I talk stock investment" in chinese, actually wogutan is a platform 
      which present US equity's informations to chinese investors, the name "wogutan" is 
      not quite a suited name.


wogutan.com features
---------------------

news:
    - original articles
    - translate IBD news

estimate(portfolio) articles:
    - watch list
    - selection list
    - other list and portfolios


wogutan.com resource needs
---------------------------
- php developer
- data/IT/content resources


wogutan.com planning in the near future
----------------------------------------
#. take over wogutan.com IT maintaining and development 
#. discuss the issues in `Questions`_, then decide what's the next planning


MarketSmith 
=============

MarketSmith products:
    - MS HK (iOS/Android/Web)
        + Mobile (Android/iOS)
        + Web (MS Global Desktop Tool)
    - MS Domestic
        + Mobile (Android/iOS/Web)
        + Web (MS Tool)


Objectives
-------------
- We need to partly take over outsourced work, especially the core modules/features, 
  including MSHK and MSDomestic
- Localize MarketSmith products
    + MS HK (iOS/Android/Web)
    + Support both simplified chinese and traditional chinese
- Fully support China A-stock and Hongkong market, including fundamental, realtime-price, ownership,
  finiancial and price estimates, etc.

Resource needs
---------------

- Buying A-stock data, see `A-stock database(CNDB)`_
- Employee recruitment, see `Recruitment`_


Panary
=======

Objectives
------------
- Partly take over outsourced work
- Localize panary products
    + Support both simplified chinese and traditional chinese language
    + Fully support China A-stock and Hongkong market 


Resource needs
---------------

- Buying A-stock data, see `A-stock database(CNDB)`_
- Employee recruitment, see `Recruitment`_



Milestones
==========

Aug 1:
    #. Jul 10: 
    #. Jul 20
    #. Jul 31

Sep 1:
    #. Aug 10
    #. Aug 20
    #. Aug 31

Oct 1:
    #. Sep 10
    #. Sep 20
    #. Sep 30

To joseph: we can put listed targets in above timelines

    - Business license done (Joseph)
    - Shanghai office come into operation (Jianwei, Hawking)
    - Hangzhou office come into operation (Jianwei, Hawking)
    - HT Conversion (Joseph, Vincent)
    - iOS/Android developer recruitment (Joseph, Vincent)
    - Network/VPN (Hawking, Jianwei)
    - wogutan.com take over (Hawking, Vincent)
        + Database
        + Web Server
        + php development
    - Contact A-stock data vendors 
    - Contact HK-stock data vendors
    - Evaluate A-stock data source (Joseph, Vincent, US colegues)
    - Evaluate HK-stock data source (Joseph, Vincent, US colegues
    - Buy A-stock data (Joseph, Vincent)
    - Buy HK-stock data (Joseph, Vincent)
    - US realtime-streaming data (USQUOTE) (Hawking, Vincent)
        + Researching on network architecture
        + contact with data vendor(Nasdaq?)
        + Researching on realtime-streaming data protocol and format
     - Hongkong realtime-streaming data (HKQUOTE) (Hawking, Vincent)
        + Researching on network architecture
        + contact with data vendor(Etnet?)
        + Researching on realtime-streaming data protocol and format
    - Data development (USDB) (Vincent)
    - Data development (CNDB) (Vincent)
        + Convert verdor's database into our database
        + Put data into WONDB or create data API for WON products backend
    - Data development (HKDB) (Vincent)
        + Convert verdor's database into our database
        + Put data into WONDB or create data API for WON products backend
