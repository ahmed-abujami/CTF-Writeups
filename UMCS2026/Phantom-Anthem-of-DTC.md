Phantom Anthem of DTC

Category: Cryptography | Difficulty: Hard | Team: Flag Hunter S

Challenge Overview
The university anthem from Dewan Tunku Canselor (DTC) was playing in an audio file called DTC_Midnight.wav, but someone had hidden a secret message deep inside the soundwaves. The task was to extract it from the stereo audio file.

Challenge Hint
True silence is only found when opposites come into contact.

Tools Used
Audacity was used for audio analysis, specifically splitting stereo channels, inverting one, and amplifying the residual signal. Morse Code World was used to decode the extracted pulse pattern. CyberChef was used for Vigenere decryption. A Python script using scipy and numpy was also written as an alternative automated solution to verify the manual Audacity work.

Solution Phase 1: Audio Forensics

Step 1: Opened DTC_Midnight.wav in Audacity. At first glance it looked like a normal stereo track playing the university anthem, with left and right channels looking almost identical.

Step 2: Split the track into two separate mono channels using Tracks then Stereo to Mono. This was necessary before flipping one channel independently.

Step 3: Inverted the phase of the right channel using Effect then Invert. The idea was that if both channels contained the same audio, flipping one would make it the exact opposite, so mixing them together would cause that shared audio to cancel out.

Step 4: Mixed and rendered both channels together using Tracks then Mix then Mix and Render. As expected, the anthem dropped out completely, leaving only the hidden difference between the two channels.

Step 5: Amplified the residual signal, which was almost completely silent at first. After amplifying, short and long rectangular blocks became visible in the waveform, which turned out to be Morse code.

Solution Phase 2: Morse to Vigenere to Flag

The Morse code pulses extracted were: dash dot dot dot, dot dot dash dot, dash dash dot dot, dot, dot dash dash, dash dot, dot dot dot dot, dot dash dash dot, dash dot dash, dot dash dot dot, dash dash, dash, dash, dash dot dot dot dot

Decoding the Morse code gave the string: BFZEJNHPKEXGNTOTH

The cipher key used was TUNKU, named after Tunku Abdul Rahman, who was the University of Malaya's first Chancellor. This connection was the answer hidden in the challenge hint all along.

Running the Morse-decoded string through CyberChef's Vigenere Decode function with the key TUNKU produced the plaintext: ILMU PUNCA KEMAJUAN

Flag retrieved: UMCS{ILMU_PUNCA_KEMAJUAN}

This phrase is the University of Malaya's motto, meaning Knowledge is the Source of Progress.

Hardships Faced
Audacity kept crashing when using the Chrome web version, so the desktop version had to be used instead. The first online Morse decoder tried kept throwing errors, requiring a switch to a working alternative. The residual signal was almost completely silent at first and was nearly missed before amplifying. Figuring out the Vigenere key required actual historical research on Tunku Abdul Rahman rather than guessing. The competition was live with multiple challenges running simultaneously, adding real time pressure.

Lessons Learned
Reading challenge hints literally matters, since the phrase about opposites coming into contact was a direct description of phase cancellation. When a tool stops working, switching quickly to an alternative keeps momentum going. Historical and contextual research can be just as important as technical skill in solving cryptography challenges. Verifying every step before moving forward prevents wasted effort and false submissions.

UM Cybersecurity Summit 2026, Team Flag Hunter S
