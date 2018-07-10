Authentication in Leihs
=======================

Known Problems in Leihs v3
--------------------------

* overcomplicated implementation, `authentication_systems` 

    * complexity has no benefits
    * obscure, security reviews are quite hard

* password authentication hash method is "broken"

* danger of stealing cookies 

* combines authentication and user management

    * goes strongly against the idea of IAM 
    * security issues 
    * leads to fragmentation 
    * complicated practically untested custom code (e.g. HSLUControler)


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

  * user and group management via sync service and API ✓

  * seperate authentication into own service (NEW PROPOSAL)


* simplify authentication code and methods: 

  * rewrite password authentication ✓ 

  * add Switch/AAI authentication ✓

    CONS:

    * Switch/AAI configuration is difficult and very time consuming
    * security: server must be configured very deligent 
    * idear goes against the grain of leihs (similar to LDAP)
    * no real sign-off 
    * I would not integrate it again in leihs
    * maybe this should (have) be(en) an external service 

  * add e-mail authentication, OPEN ?
    * very cheap to implement 
    * needs no additional setup from the administrator (email setup is required at any rate)
    * quite secure
    * SIMPLE and AVAILABLE

  * add LDAP authentication, OPEN ?

    * full featured LDAP authentication is out of scope (online like Gitlab)
    * LDAP user and group management is out of scope (complexity and security, Basel)
    * simple bind authentication is feasible (see OWASP)

    PROS: 

    * "best practice" and "industry standard" 
    * marketing 
    * project managers can fill check mark


    CONS:

    * there is a high(er) security requirement involved with LDAP 
      * org. passwords pass through leihs, logging, leaks
      * LDAP injection

    * if LDAP auth would not exist there is no way it would be accepted with 
      todays accepted security standards 

    * without user and group management LDAP authentication might not be much useful


  * guide user through authentication 
    * two-step: first request email, than present available options
    * recently implemented and enforced by: google, microsoft, amazon, ....
    * really not alternative, but
       * we can shortcut steps for most ZHdK users, 
       * or disable two-step for ZHdK only (if we like to confuse users)
    

leihs-auth Service
------------------

provides: 

* UI/UX for signing in
* creating and destroying user sessions
* evaluate scopes (for tokens and sessions), benefit e.g. read only "switch to"
* providing per request session or token evaluation for other 
    leihs services via HTTP requests (optionally as reverse proxy)
* optional access point for an external sign-in service: API to provide sign-in
  via HTTP to organizational services

optional: 
* user namespace
  * manage sessions i.e. cookies 
  * manage API tokens
  * change password and possibly some other user attributes 
  * view group and role membership

Codebase as small as possible with only a few dependencies
  * fairly easy to review (for security)
  * smaller surface for security attacks 

Code is already partly implemented in Admin/API: extract and extend



External Sign-In Service 
------------------------
* optional 
* quite simple to implement, no UI required
* can be combined with sync service
* real single-sign-on is possible
* can replace sync service: create entities on request basis;
  not recommended (see IAM etc) but can make things quite simple
* payload: user-id (or email, or org_id), lifetime of cookie, target_url, 
    timestamp or onetime token (against replay attacks), send via query param 
    of redirect (e.g. signed or encoded json web token)
    

Notes: 
------

^email1: e-mail service rewrite consumeable for all services
