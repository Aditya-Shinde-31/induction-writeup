#COEP CyberCell SY Inductions 2026 - Mini CTF Write-up

Hello! I am very new to the world of cybersecurity, and this induction CTF gave me a great opportunity to explore what "flags" actually are and the different ways to hunt them down. Overall, the experience was fantastic, and I felt like a newbie digital detective finding hidden hints to crack a case!

Here is a documentation of my methodology and solutions for the challenges.

Challenge 1: The Basics (Web Inspector)

Concept Learned: Web page source code is visible to the client.

Solution: This was the easiest challenge. I learned that what we see on a webpage is just the rendered view. By right-clicking and selecting "Inspect" (or viewing the page source), I checked the underlying HTML code and found the flag hidden right at the bottom.

Flag: COEP{view_source_is_your_friend}

Challenge 2: Mystery String

Concept Learned: The difference between Encoding and Encryption.

Solution: I was given a scrambled string: Q09FUHtiYXNlNjRfaXNfbm90X2VuY3J5cHRpb259. Because it ended with alphanumeric characters and padding, it looked like Base64. I learned that Base64 is encoding (translating data format), not encryption (which requires a secret key to decipher). I used CyberChef / the base64 --decode command in the terminal to decode the string.

Flag: COEP{base64_is_not_encryption}

Challenge 3: Picture Perfect

Concept Learned: Files carry hidden luggage called Metadata.

Solution: The flag was hidden in a photograph! I didn't know that flags could be stored inside the metadata of an image. I downloaded the photo.jpg forensic file and used an EXIF extraction tool to inspect the hidden container headers and tags, revealing the secret string.

Flag: COEP{metadata_never_lies}

Challenge 4: Polite Robots

Concept Learned: How web crawlers interact with robots.txt.

Solution: I used to wonder if we could hack website passwords using the inspect feature, but this challenge taught me about directory access. Search engines use a file called robots.txt to know which pages not to index. Ironically, developers sometimes list their secret vaults here! I inspected the site's robots.txt, found the Disallow path for /mini-ctf/s3cr3t-vault-7f3a/, and navigated to that URL in my browser to breach the vault.

Flag: COEP{robots_know_secrets}

Challenge 5: Where Was This Taken?

Concept Learned: OSINT (Open-Source Intelligence) and visual geolocation.

Solution: This challenge was a fun observational one. All GPS metadata was stripped from the image, so I had to rely on visual clues like the 1865 heritage stone facade and arches. Since it was on our very own COEP campus, I quickly identified the historic landmark and formatted its name according to the club's flag syntax.

Flag: COEP{main_building}

Challenge 6: Not What It Seems

Concept Learned: File Signatures (Magic Bytes) govern true file formats, not extensions.

Solution: This was a real "wondering" moment for me—how can changing a .jpg to a .zip reveal more than what we see? A suspect left behind mystery.jpg, but it wouldn't open. By checking the file's first few bytes (the Magic Bytes), I noticed 50 4B 03 04 (ASCII: PK..), which actually indicates a ZIP archive. I renamed the file extension to .zip and extracted it to read the enclosed flag.txt!

Flag: COEP{not_every_jpg_is_a_jpg}

Note: I utilized AI tools (Gemini) strictly to help format, structure, and grammar-check my raw notes for this GitHub Markdown document, as permitted by the induction rules.
