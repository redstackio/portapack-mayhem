# [**Red**Stack.io](https://www.redstack.io) Labs presents...
## A backported improvement of the upstream eried/portapack-mayhem v1.6.0 stable.

Enabling support for the latest batch of r9 hackrf one devices, QFP100 china knockoffs, and working hackrf mode, without needing to run nightly.

## These may not be the droids you are looking for! If you are looking for portapack-mayhem's main repo, find it here: [https://github.com/eried/portapack-mayhem](https://github.com/eried/portapack-mayhem)

If you acquired your hackrf/portapack combo from the [recommended aliexpress link](https://s.click.aliexpress.com/e/_DmU7GQX) detailed in the [what to buy section](https://github.com/eried/portapack-mayhem#what-to-buy), it will not work with v1.6.0 stable as it is now shipping an r9 hackrf, and so is too new. This probably is true for any genuine r9 device too, but we ([**Red**Stack.io](https://www.redstack.io) Labs) only have the one linked in the repo. Until such a time as upstream cuts a stable release, this version will work as a stable for this new variety of the device.

Contained within the [release bundle](https://github.com/redstackio/portapack-mayhem/releases/tag/v1.6.1-rs):

- Compiled firmware from the v1.6.1-rs tag/branch of this repo.
- Upstream hackrf dfu and firmware bundle.

You'll also want the SD Card content for v1.6.0 from here: https://github.com/eried/portapack-mayhem/releases/tag/v1.6.0

# Warning: If you use this firmware, it's unlikely the developers in discord will offer any support, as they consider it a _zOmBiE bUiLd_

That said, do open issues for the lack of r9 hackrf support in stable in their repo and perhaps they'll cut a point release to break the pain cycle as the number of these devices increases now that ali vendors are shipping them.

### Important note about r9, h2+, and google search results that will cause you misery
It is important, if you have an r9, that you don't use jumbo77's 1.43 release. It won't work. Nor will the `hackrf_one_usb.dfu` and `hackrf_one_usb.bin` firmware in the v1.6.0 release bundle, as it predates the merge of the r9 release code from GSG's repo. You **must** use the [Great Scott Gadgets release](https://github.com/greatscottgadgets/hackrf/releases/tag/v2023.01.1) firmware for dfu recovery or you will end up with a hackrf with flashing lights and a pained expression on your face.

I have helpfully included both the dfu and bin for the hackrf v2023.01.1 release in this release file, so you _can_ use the ones from this zipfile.

### Firmware apply process:

1. Apply upstream hackrf firmware:  
`hackrf_spiflash -i -w hackrf_one_usb.bin`
2. Restart hackrf then patch with portapack-mayhem firmware:  
`hackrf_spiflash -i -w portapack-h1_h2-mayhem.bin`
3. Disconnect from PC, then power on.
4. You should see the splash and then have a working portapack.

If you see a black screen on startup, power off the portapack then hold the right button and power back on. Repeat with the left/up/down/center button until LCD works.

### If you have already bricked your hackrf, you will need to use dfu to recover it.

1. Disassemble the hackrf + portapack.
2. Connect hackrf only to PC.
3. Hold DFU and Reset buttons then release reset and the light closest to the antenna port should glow faintly.
4. `dfu-util -l` to confirm the presence of the device
5. Apply upstream base firmware to the RAM:  
`dfu-util --device 1fc9:000c --download hackrf_one_usb.dfu --reset`
6. If you now have a set of solid and bright lights at the top of the hackrf this step worked, and you can now immediately flash with upstream base firmware beginning at step 1 of the firmware apply process above.
7. After you have patched with portapack firmware, reassemble the device, and you should be able to power it on.
8. Test entry to hackrf mode. Confirm the blue screen appears properly. Confirm the device appears in the device list when connected to your PC
9. Disconnect from USB and confirm the device returns to portapack mode.

```
                            
                            _ood>H&H&Z?#M#b-\.
                        .\HMMMMMR?`\M6b."`' ''``v.
                     .. .MMMMMMMMMMHMMM#&.      ``~o.
                   .   ,HMMMMMMMMMM`' '           ?MP?.
                  . |MMMMMMMMMMM'                 `"$b&\
                 -  |MMMMHH##M'                     HMMH?
                -   TTM|     >..                   \HMMMMH
               :     |MM\,#-""$~b\.                `MMMMMM+
              .       ``"H&#        -               &MMMMMM|
              :            *\v,#MHddc.              `9MMMMMb
              .               MMMMMMMM##\             `"":HM
              -          .  .HMMMMMMMMMMRo_.              |M
              :             |MMMMMMMMMMMMMMMM#\           :M
              -              `HMMMMMMMMMMMMMM'            |T
              :               `*HMMMMMMMMMMM'             H'
               :                MMMMMMMMMMM|             |T
                ;               MMMMMMMM?'              ./
                 `              MMMMMMH'               ./'
                  -            |MMMH#'                 .
                   `           `MM*                . `
                     _          #M: .    .       .-'
                        .          .,         .-'
                           '-.-~ooHH__,,v~--`'

    __  __           __      __  __            ____  __                 __
   / / / /___ ______/ /__   / /_/ /_  ___     / __ \/ /___ _____  ___  / /_
  / /_/ / __ `/ ___/ //_/  / __/ __ \/ _ \   / /_/ / / __ `/ __ \/ _ \/ __/
 / __  / /_/ / /__/ ,<    / /_/ / / /  __/  / ____/ / /_/ / / / /  __/ /_
/_/ /_/\__,_/\___/_/|_|   \__/_/ /_/\___/  /_/   /_/\__,_/_/ /_/\___/\__/

      ░░░░░░░█████╗░██████╗░██╗░░██╗███████╗██╗░░░░░██╗░█████╗░
      ░░░░░░██╔══██╗██╔══██╗██║░░██║██╔════╝██║░░░░░██║██╔══██╗
      █████╗██║░░██║██████╔╝███████║█████╗░░██║░░░░░██║███████║
      ╚════╝██║░░██║██╔═══╝░██╔══██║██╔══╝░░██║░░░░░██║██╔══██║
      ░░░░░░╚█████╔╝██║░░░░░██║░░██║███████╗███████╗██║██║░░██║
      ░░░░░░░╚════╝░╚═╝░░░░░╚═╝░░╚═╝╚══════╝╚══════╝╚═╝╚═╝░░╚═╝
                                               └──RedStack Labs
```
