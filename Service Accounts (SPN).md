# Service Accounts (SPN)

Service accounts are non-human accounts that are used to run services or applications. Service accounts often have elevated privileges, their passwords are rarely (if ever) changed, and they are rarely monitored by security teams. This allows hackers to leverage a compromised service account for an extended period of time, thus making them an attractive target.

Each service instance has a unique identifier called a Service Principal Name (SPN), which also includes information about what the account is used for and its location. Any authenticated user can log in to an Active Directory domain and submit a request for a ticket-granting service (TGS) ticket for any service account by specifying its SPN value.

They can then extract the service account’s password hash and attempt a brute force attack to obtain the plaintext password, with little risk of being detected or locked out of their account.
