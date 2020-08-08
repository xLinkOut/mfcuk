# MiFare Classic Universal toolKit (MFCUK)
{ caption }

## Install
### Prerequisites
* [LibNFC 1.8.0](https://github.com/nfc-tools/libnfc/releases) 
* _pkg-config_, _automake_ and _libtool_

### Compiling
```bash
autoreconf -is
./configure
make
(sudo) make install # optional
```

### Running
Basic usage, recover key A for sector n.0, with a verbosity level of 2: `mfcuk -C -R 0:A -v 2`
Weak card, recover key B for sector n.1 with a verbosity level of 3: `mfcuk -C -R 1:B -w 6 -v 3`

## AUTHOR
Andrei Costin <zveriu@gmail.com>, http://andreicostin.com
### CONTRUBUTORS
* Romuald Conty <romuald@libnfc.org> - porting to libnfc 1.3.x, 1.4.x, 1.5.x
* Nethemba Core Team <mifare@nethemba.com> - core AC, AM, configure and packaging
* DrSchottky <> - weak cards patch, fix 0x03 error

## WEAK CARDS PATCH
mfcuk does not handle cards that always respond with NACK to failed auth attempts. This is the cause of 0x03 error on some cards.
@Stewart8 [solved the problem](https://github.com/nfc-tools/mfcuk/issues/39) and @DrSchottky applied his patch to mfcuk source with some adjustments, like:
- no more crashes with 1M+ candidates
- configurable maxhi/lo threshold
- "weak card mode" can be turned on/off selectively
To use mfcuk in weak card mode add '-w threshold' to cmdline args. Suggested threshold val: >=6

## TODO
0. Remove dead-code/commented block after testing
1. Proper error handling in some cases (not critical errors, but nice to have checks in place)
2. Integrate with MFOC into MFCUK
3. Create sort of GUI
4. Improve the performance (though not bad)
5. Optimize bits operations
6. Periodically save the state (or most important part of it at least) such as of Nt/Nr arrays, etc., so that it can later be resumed on the same card
7. Calibration methodology and routine for MFCUK to determine best field on/off delays so that it generates the lowest entropy for tag's Nt values

## LICENSE
GPL. See `license/LICENSE` for more information.

## BIBLIOGRAPHY (no specific order)
1. [WPMCC09] - "Wirelessly Pickpocketing a Mifare Classic Card"
2. [ESO08] - "2008-esorics.pdf"
3. [ESOSL08] - "2008-esorics-slides-updated.pdf"
4. [KON08] - "2008-koning-thesis.pdf"
5. [VER08] - "2008-verdult-thesis.pdf"
6. [PATMC] - "A Practical Attack on the MIFARE Classic.pdf"
7. [NCOURFIDSEC09] - "mifare_courtois_rfidsec09.pdf"
8. [MFCLTRB09] - "MifareClassicTroubles.ppt"
9. [TEEP08] - "p2008-teepe-classic_mistakes.pdf"
10. [RFIDSANJ] - "RFID Attacks_WCA_San_Jose.pdf"
11. [ROSS] - "rossum-mifare.pdf"
12. [PLOTZ08] - "SAR-PR-2008-21_.pdf"
13. [ROSSSASG] - "SASG35_Peter_v_Rossum_Mifare.pdf"
14. [DARK2009] - "THE DARK SIDE OF SECURITY BY OBSCURITY and Cloning MiFare Classic Rail and Building Passes, Anywhere, Anytime"

### KUDOS and HATS-OFF to (no specific order) (for all the knowledge, time spent researching and all the things)
 - blapost@gmail.com - this man is a genius and a technical artist. crapto1 3.1 is the horse power of this tool. PS: you somehow resemble I.C.Wiener anonymous&smart hacker
 - Roel and RConty @ libnfc/proxmark - these guys are true advisers, helpful. Thanks for providing a powerfull platform for NFC
 - N.Curtois - also a crypto-artist in differential analysis. The 29bit prefix attack is pure genius of theoretical analysis.
 - RU University Staff for working out different aspects and papers for Crypto1 analysis
 - Nohl, Plotz, Evans - how the "F" did you get those slicers and microscopes :))?
 - Milosch M et al. - for pushing the limits for open-source hardware (OpenPCD and OpenPICC)
 - Jonathan Westhues - for giving the open-source community the: Proxmark schematics/sources and RFID knowledge
 - Nethemba team - for first open-source/GPL nested authentication attack key recovery implementation in MFOC
 - hat, schwa226, pgrahamm, marcus2608, phadom - for useful samples, advices, traces and all the things
