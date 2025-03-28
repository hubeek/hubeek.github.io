# Meteor setup project with accounts

_Status: Published_
_Created: 2017-02-19 15:44:54_
_Tags: raspberry pi_

meteor --version
meteor update --release 1.6.1

<h3>Router:</h3>
 meteor add iron:router

<h3>Bootstrap:</h3>
meteor add twbs:bootstrap

<h3>Accounts:</h3>
meteor add accounts-ui accounts-password
meteor add joshowens:accounts-entry
meteor npm install --save bcrypt
meteor add check

adjust client with code from
https://github.com/Differential/accounts-entry/
