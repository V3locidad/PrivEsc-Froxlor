# PrivEsc-Froxlor

It is possible to perform a privilege escalation with the Froxlor admin account, allowing commands to be executed as root on the server.

Poc

First, you need to log in to the Froxlor admin interface.

In the feature available for PHP-FPM versions, it is possible to change the restart command, which is executed as root. This allows copying the id_rsa file from the root directory to /tmp. Then, by changing the file permissions (e.g., with chmod 777 /tmp/id_rsa), it becomes possible to later root the server using the key.

Default command in PHP-FPM

<img width="1156" alt="Capture_decran_2024-09-09_a_15 34 04" src="https://github.com/user-attachments/assets/d0967193-df59-41cf-8c40-a66d4a9d9384">

Command to copy the root RSA key to /tmp

<img width="1118" alt="Capture_decran_2024-09-09_a_15 38 43" src="https://github.com/user-attachments/assets/2a3fe9e2-bc7f-46da-b2f7-9000007438d8">

Service restart to execute the command

<img width="1113" alt="Capture_decran_2024-09-09_a_15 39 36" src="https://github.com/user-attachments/assets/d043dc65-fb3c-4fb6-98e0-8d3d55840211">

Change the permissions on the previously copied key, then restart the service again to execute the command.

<img width="1113" alt="Capture_decran_2024-09-09_a_15 39 14" src="https://github.com/user-attachments/assets/927875da-c1c5-42ef-90bb-f5be54c75c44">


# Implications and Additional Possibilities:

- Permanent root access: Once the SSH key is retrieved, it’s possible to gain persistent root access, enabling complete and long-term control over the server.

- Executing other commands as root: Beyond copying files, modifying the restart command can be leveraged to execute various other root-level commands. For instance, it allows adding users with elevated privileges, changing critical configurations, or installing remote access tools.

- Exfiltration of sensitive data: With root access, it becomes possible to access sensitive files or exfiltrate critical data that would otherwise be protected.

- Additional persistence: Startup scripts or scheduled tasks can be configured to ensure long-term access, even if root SSH access is restricted later.

This attack vector highlights the importance of securing commands executed with elevated privileges, especially in configurations accessible through a web interface.
