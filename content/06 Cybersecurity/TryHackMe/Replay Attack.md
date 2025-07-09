# Authentication in the Digital World

The situation on the network is even more challenging to secure. If the user sends their username and password in cleartext, anyone capturing traffic on the network can learn the username and the password. How can we prevent them from learning the login credentials?

The server and the user can agree on a fixed secret key. Instead of sending the password in cleartext, the user encrypts it using the selected secret key. Whenever users want to log in, they send their username and password encrypted using their assigned secret key. Now the attacker should never be able to learn the password, right? Unfortunately, although they won’t be able to know the password, they can still authenticate. This attack is shown in the figure below.

This figure shows an attacker using a replay attack. The attacker only resends the same packet the legitimate user sent earlier and gains access to the server.

Although the attacker does not know the password, they can still authenticate by replaying the same response. This attack is considered a replay attack. Is there anything we can do to fix this?

# Making the Challenge Response Unique

An encrypted password that is always the same value is easy to circumvent. We need some mechanism to ensure that the response won’t be reused repeatedly. One approach would be to use the current time and date as part of the response. In other words, the user would send an encryption of the current time (and date) along with the password. Although this requires both parties to synchronise their clocks, it ensures that the response is only valid for a brief time, usually in milliseconds.

This task aims to shed some light on some of the challenges related to authentication and authentication protocols. Many other vulnerabilities can make their way into authentication protocols; however, it is beyond the scope of this room.