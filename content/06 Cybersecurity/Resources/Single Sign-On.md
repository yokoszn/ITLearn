Users need to access various sources to carry out their daily work routines. For instance, they would need to access their email, shared files, and printers, among others. Accessing these resources requires the user to have login credentials for successful authentication. The number of different usernames and passwords makes it quite challenging, especially if the users are rightfully not reusing the same password across multiple systems.

Single Sign-On (SSO) tackles this problem. Instead of a user having to remember multiple usernames and passwords, they only need to remember a single set of login credentials. They can authenticate themselves to one system, granting them access to the other systems necessary for their work.

![[Pasted image 20241114160956.png]]

This figure shows a user authenticating using Single Sign-On (SSO) and gaining access to three servers.

Traditionally, a user must create several passwords, such as a password to log in to their computer, another password to check their email, and a third password to access a file share. Recalling this number of passwords can be cumbersome, especially since, ideally speaking, a password should not be reused. The better approach would be to require the user to log in once and grant them access to all the needed services; that’s what SSO does.

SSO allows organisations to authenticate users once before granting them access to the resources required for their work. We can achieve many advantages from this. We will mention a few.

- One strong password: Expecting a user to remember a single strong password is more acceptable than asking them to remember ten different strong passwords.
- Easier MFA: Adding MFA to every different service is a humongous task to accomplish and maintain. With SSO, MFA needs to be enabled and configured once.
- Simpler Support: Support requests like password reset become more straightforward as they are now confined to a single account.
- Efficiency: A user does not need to log in every time they need to access a new service.