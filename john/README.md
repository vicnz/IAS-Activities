# Using John The Ripper to crack passwords

### Installation

You can download the `john` files from [https://www.openwall.com/john/]:john

#### Step 1.

In Windows download the zip file. [https://www.openwall.com/john/k/john-1.9.0-jumbo-1-win64.zip]:x64, or if your using **x32** [https://www.openwall.com/john/k/john-1.9.0-jumbo-1-win32.zip]:x32

#### Step 2.

Extract the zip file in the `C:/` drive of your pc.

#### Step 3.

Add the folder `C:/john/run` to the system environment variables in the `PATH` variable

How to add folder into system environment variables. https://youtu.be/WbRlwNPKOSY?si=YvXGMtxmw8lGubf1

#### Step 4.

Restart you `Terminal` or `CMD CLI` or `PowerShell CLI`

#### Step 5.

Check if the `john` command is available in the terminal by  running

```cmd
john -v
```

***

## Convert ZIP to john format

John the Ripper requires the password hash to be in a specific format. To convert the ZIP file’s password hash into the appropriate format, use the `zip2john` utility that comes with John the Ripper. Open a terminal and navigate to the directory containing the ZIP file. Run the following command:

```cmd
zip2john your_zip_file.zip > zip.hash
```

With the password hash extracted and saved, you can now initiate the password cracking process using John the Ripper. In the terminal, run the following command:

```cmd
john zip.hash
```

> In **Windows** the format of the outputted `zip.hash` may produce error due to invalid encoding.  Run this command to convert the file from `UTF-16` to `UTF8`
>
> ```powershell
> Get-Content -Path "zip.hash" | Out-File -FilePath "your_encoded.txt" -Encoding utf8
> ```
>
> then run:
>
> ```powershell
> john your_encoded.txt
> ```

> Note: if you are seeing an notice message when running `john`
>
> ```powershell
> Using default input encoding: UTF-8
> Loaded 1 password hash (ZIP, WinZip [PBKDF2-SHA1 256/256 AVX2 8x])
> No password hashes left to crack (see FAQ)
> ```
>
> Go inside the folder `C:/john/run` and look for the `john.pot` file then delete it.
>
> Then run the `john` command again.

***

## Dictionary Mode

In dictionary mode, we will provide John with a list of passwords. John will generate hashes for these on the fly and compare them with our password hash.

After performing the commands above (*except the `john`*) prepare your password list file this can come from `.txt` or `.lst` files.

```powershell
john --wordlist=C:/john/password-list.txt your_encoded.txt
```

Here in our case we added an additional parameter called `--wordlist` we provided the location of the a dictionary lists file in this option (*in our case is located at`C:/john/password-list.txt`*).

`john` will use this list of passwords to find matching values.

