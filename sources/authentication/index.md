Authentication in Leihs
=======================

Known Problems in Leihs v3
--------------------------

0. overcomplicated implementation, `authentication_systems` 
    0. complexity has no benefits
    0. obscure, security reviews are quite hard

0. password authentication hash method is "broken"

0. danger of stealing cookies 

0. combines authentication and user management
    0. goes strongly against the idea of IAM 
    0. security issues 
    0. leads to fragmentation 
    0. complicated practically untested custom code (e.g. HSLUControler)


Fixes in Leihs v4
-----------------

* Most of the cookies issues. 
* Patched security issues we became aware of.

Relly nothing else. 


Proposedand and partly implemented changes for Refactoring (Leihs v5)
---------------------------------------------------------------------

* Seperate authentication and user (as well as group) management. 

  * implement the core idea behind IAM

  * enable requested features (in the future)

  * user and group management via sync service and API.  
    * done for users
    * API done for groups, sync pending

  * seperate authentication into own service (new)


* simplify authentication code and methods: 

  * rewrite Password Authentication (done)

  * add Switch/AAI authentication (done)

  * add e-mail authentication:
    * very cheap to implement (see ^email1)
    * needs no additional setup from the administrator (email setup is required at any rate)
    * quite secure 
    * SIMPLE and AVAILABLE 

  * add LDAP authentication (maybe) 

    * full featured LDAP authentication is out of scope (online like Gitlab)
    * LDAP user and group management is out of scope (complexity and security, Basel)
    * simple bind authentication is feasible (see OWASP)

    there are still quite some drawbacks:

    * there is a high(er) security requirement involved with LDAP 
      * org. passwords pass through leihs, logging, leaks
      * LDAP injection

    * without user and group management LDAP authentication might not be much useful

  * guide user through authentication 

    * two step: first request email, than present available options

    * recently implemented and enforced by: google, microsoft, amazon, ....
    

leihs-auth Service
------------------

provides: 

* UI/UX for signing in
* creating and destroying user sessions
* evaluate scopes (for tokens and sessions), benefit e.g. read only "switch to"
* providing per request session or token evaluation for other 
    leihs services via HTTP requests (optionally as reverse proxy)
* optional access point for an external sign-in service 

Codebase as small as possible with only a few dependencies
  * fairly easy to review (for security)
  * smaller surface for security attacks 

Code is already partly implemented in Admin/API: extract and extend

Possible to add API to provide sign-in via HTTP to organizational services.


External Sign-In Service 
------------------------
* optional 
* quite simple to implement, no UI required
* can be combined with sync service
* real single-sign on is possible
* can replace sync service: create entities on request basis;
  not recommended (see IAM etc) but can make things quite simple
* payload: user-id (or email, or org_id), lifetime of cookie, target_url, 
    timestamp or onetime token (against replay attacks), send via query param 
    of redirect (e.g. signed or encoded json web token)
    

Notes: 
------

^email1: e-mail service rewrite consumeable for all services
