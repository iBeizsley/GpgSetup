0. Install GPG:
      
    0.1. Check whether GPG is already installed (`gpg` in console/terminal).
  
    0.2. **[Windows]** Download + install: https://www.gpg4win.org/.

    0.3. **[Mac]** Install via Homebrew:

    Install Homebrew if necessary: `ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
	
    `brew install gnupg`
    
    0.4. **[Linux]**
    
    **Red Hat / CentOS:** `yum install gnupg`
    
    **Ubuntu / Debian:** `apt-get install gnupg`

1. Generate key w/ name + email.

   Should match GitHub email address + name. Private GH emails are recommended, found at https://github.com/settings/emails, eg: `12345678+aUsername@users.noreply.github.io`.
    ```
    gpg --full-generate-key
    Enter
    4096
    Enter (Or specify expiration)
    Confirm
    Full Name
    Email
    Optional comment (eg GitHub)
    Confirm
    ```

2. List keys:
    ```
    gpg --list-secret-keys --keyid-format LONG
    ```

3. Get key ID from output (eg `AAAAAAAAAAAAAAAA` from):
    ```
    ---------------------------------------------------------
    sec   rsa4096/AAAAAAAAAAAAAAAA 2020-01-01 [SC]
          0000000000000000000000000000000000000000
    uid                 A Person <12345678+aUsername@users.noreply.github.io>
    ssb   rsa4096/BBBBBBBBBBBBBBBB 2020-01-01 [E]
    ```

4. Set .gitconfig file (eg `C:/users/[USER]/.gitconfig`) to:
    ```
    [user]
    	email = 12345678+aUsername@users.noreply.github.io
    	name = A Person
    	signingKey = AAAAAAAAAAAAAAAA
    [commit]
    	gpgSign = true
    ```
    4.1. **[Windows]** Append above file with (changing path as necessary):
    ```
    [gpg]
    	program = C:\\Program Files (x86)\\GnuPG\\bin\\gpg.exe
    ```
    Note: `gpgSign = true` signs all commits; alternatively, this section can be left out, and users can manually choose which commits to sign by adding `-S` in their commit command.

5. Export public key:
    ```
    gpg --armor --export AAAAAAAAAAAAAAAA
    ```

6. Add export to GH at https://github.com/settings/keys:
    ```
    -----BEGIN PGP PUBLIC KEY BLOCK-----
    EVERYTHING INSIDE
    -----END PGP PUBLIC KEY BLOCK-----
    ```
