# Bug report

Considering the attacker already had access to the randomized names of the anonymized tables, this bug enabled the attacker to view the tables outside his user group. 

A simple interception on the GET request made using burpsuite, the hacker can edit the end-point and change the name of the table to view any table in the anonymized database. 

This however worked only with anonymized databases and not the raw CSV as there was a second privilege check.
