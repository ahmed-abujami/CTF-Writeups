Zip-a-Dip-Doo-Dah

Category: Web Exploit | Difficulty: Medium | Points: 70

Challenge Overview
A web app called "Zippy Scanner Enterprise" allows uploading zip archives, claiming to inspect and block malicious content before extraction.

Vulnerability
The platform's malicious content filter relies on filename and string signature matching rather than analyzing actual file behavior. Splitting the malicious PHP payload string into separate variables was enough to bypass detection.

Steps

Step 1: Built a PHP webshell payload. The payload code was: <?php system($_GET["cmd"]); ?>

Step 2: Bypassed the antivirus and signature filter by splitting the payload string into two variables and concatenating them before writing to file, which avoids the literal blocked string pattern. This was done in PowerShell by setting $a equal to the first half of the payload and $b equal to the second half, then writing them combined into Shell.PHP using Set-Content.

Step 3: Compressed the payload file into a zip archive using PowerShell's Compress-Archive command, targeting Shell.PHP and outputting exploit.zip.

Step 4: Uploaded exploit.zip to the Zippy Scanner Enterprise platform. It extracted successfully and returned a link to the uploaded Shell.PHP file.

Step 5: Accessed the webshell through the extracted file path and passed a command through the cmd GET parameter to read the flag, using a URL like the challenge host followed by uploads, the upload directory, Shell.PHP, and then ?cmd=cat%20/flag*

Step 6: Flag retrieved: UMCS{4cbe98be-7f52-4454-a274-cab8be62b452}

Lessons Learned
Filename and string signature based malware filters are trivially bypassed by splitting or obfuscating payload strings before writing to disk. Any file upload and extraction feature that places files in a web accessible directory is a critical remote code execution risk if executable extensions like .php aren't blocked or sandboxed. Defense should validate file content and execution context, not just match known bad strings.

UM Cybersecurity Summit 2026 , Team Flag Hunter S
