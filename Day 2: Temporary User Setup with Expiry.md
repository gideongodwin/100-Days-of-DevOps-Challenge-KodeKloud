## Day 2: Temporary User Setup with Expiry

#### Task Details:
As part of the temporary assignment to the `Nautilus` project, a developer named siva requires access for a limited duration \
To ensure smooth access management, a temporary user account with an expiry date is needed. Here's what you need to do: \
- Create a user named `siva` on `App Server 1` in Stratos Datacenter. Set the expiry date to `2026-12-07` ensuring the user is created in lowercase as per standard protocol.

#### STEPS:
1. Connect to App Server 1 \
  `ssh tony@stapp01` 
- When prompted, enter the password for user `tony`


2. Create the User with the expiry date `2026-12-07` \
  `sudo adduser -e 2026-12-07 siva`

