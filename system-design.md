# System design

## instagram 

need a gateway server to deal with 

client use HTML protocol 

How to reroute to different server side



1. profile

   create profile =&gt; gateway server \(use token, authocation \)-&gt; profile server \(create profile\) -&gt; create account 

 



1. store, share images



image -&gt; store in file system. separate store images url and image in storage \(cloud, distribute file system  \) and store url \(CDN\) 

1. more cheaper 2. faster 3. can use CDN
2. like, comment

use different table 

use active table to control different action

1. follow someone

   table : follow userid followed id 



1. publish news feed

many server : use load balance \(consistency hashing\)

client =&gt; news feed -&gt; post and follow 

notification =&gt; from follow 

long polling

clerebrity let user poll get new notify



![](.gitbook/assets/screen-shot-2020-11-08-at-4.15.52-pm.png)

![](.gitbook/assets/screen-shot-2020-11-08-at-4.19.47-pm.png)

1. message 

effect way is use peer to peer protocol tcp use connect id to connect with server to connect \(use session\)



1. 


