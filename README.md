# service-escalation-executable-files

*credit to HTM* | https://tryhackme.com/room/windowsprivescarena

1) Start PowerShell:

`C:\Users\user> powershell -ep bypass`

[![Image of get-acl](https://github.com/kam1n0/service-escalation-executable/blob/master/tmp_upload/get-acl.png)](#)

2) Start *pyftpdlib* on Kali:

[![Image of pyftpdlib](https://github.com/kam1n0/service-escalation-executable/blob/master/tmp_upload/pyftpdlib.png)](#)

* Note: if pyftpdlib is not installed do the following:

[![Image of install](https://github.com/kam1n0/service-escalation-executable/blob/master/tmp_upload/install.png)](#)

3) Copy *windows_service.c* from windows machine:

[![Image of ftp](https://github.com/kam1n0/service-escalation-executable/blob/master/tmp_upload/ftp.png)](#)

* Observe *windows_service.c* was received by the FTP server on Kali

[![Image of upload](https://github.com/kam1n0/service-escalation-executable/blob/master/tmp_upload/upload.png)](#)

4) Edit *windows_service.c* to include the command to add a new user:

[![Image of edit](https://github.com/kam1n0/service-escalation-executable/blob/master/tmp_upload/edit.png)](#)

5) Compile *windows_service.c*:

[![Image of compile](https://github.com/kam1n0/service-escalation-executable/blob/master/tmp_upload/compile.png)](#)

* Note: install *gcc-wingw-w64* if it is not installed

[![Image of gcc_install](https://github.com/kam1n0/service-escalation-executable/blob/master/tmp_upload/gcc_install.png)](#)

6) Transfer *x.exe* to windows victim machine:

[![Image of transfer](https://github.com/kam1n0/service-escalation-executable/blob/master/tmp_upload/transfer.png)](#)

7) Copy *x.exe* to C:\Temp:

[![Image of copy](https://github.com/kam1n0/service-escalation-executable/blob/master/tmp_upload/copy.png)](#)

8) Execute *x.exe*::

[![Image of execute](https://github.com/kam1n0/service-escalation-executable/blob/master/tmp_upload/execute.png)](#)

- Here is the breakdown of this*reg add* command:
  - 'reg add' is adding to the 'regsvc' registry
  - 'v' is adding a registry value of 'ImagePath'
  - 'ImagePath' is a registry key that contains the path of the drivers image file
   - If we place an executable here, when we tell the service to start in the ImagePath, it is going to run the executable
  - 't' is of the type REG_EXPAND, which is saying "this is a string value"
   - The "string value" is the /d (data) C:\temp\x.exe
  - 'f' says to not provide any prompts

9) In the command prompt, type *'sc start regsvc'*:

[![Image of start](https://github.com/kam1n0/service-escalation-executable/blob/master/tmp_upload/start.png)](#)

10) We can then execute *net local group administrators*, and see that our new administrator user 'backdoor' was added:

[![Image of backdoor](https://github.com/kam1n0/service-escalation-executable/blob/master/tmp_upload/backdoor.png)](#)
