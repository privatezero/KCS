# KCS
Information and software from (http://dxforth.netbay.com.au/#kcs) where it was listed under the following license:

"Disclaimer: The projects presented here are experimental in nature. They may be incomplete, not fully tested or contain defects.
Being free software, it is provided 'as is' and without any warranty. Use of these projects or information is strictly at your own risk
and responsibility. Project material written and created by the author is Public Domain; any non-original or reference material
included may be subject to copyright by their respective owners."



# KCS README
KCS - A Kansas City Standard/CUTS Tape Conversion Utility

This is for all you old-timers that still have computer programs
on cassette!

One of the most popular early ways to store computer programs on
audio cassettes was the Kansas City Standard (also known as the
'BYTE standard'). Developed in 1975, it uses an encoding scheme
where a '0' bit is represented as 4 cycles of 1200Hz and a '1'
bit as 8 cycles of 2400Hz. The data rate is 300 bits per second.
Computers which used the Kansas City Standard include S100-based
systems, PT SOL-20, Ohio Scientific C1P/Superboard II, Compukit
UK101, Acorn ATOM and many others.

The "KCS" utility allows programs stored on cassette tape using
either the "Kansas City Standard" or "CUTS" (Processor Technology
Computer Users Tape Standard) to be decoded to a program file.
The reverse process - converting a program file to an audio
wavefile is also possible, allowing one to produce perfectly
regenerated cassettes. KCS works with 8-bit mono WAV, VOC or RAW
audio files recorded at 22050 samples per second. A variety of
serial formats are allowed including 7 or 8 bit data, 1 or 2 stop
bits, odd/even or no parity.


NOTES

1. Decoding

 a) The audio file MUST be an 8-bit mono file recorded at 22050
    samples per second. Any other format will result in failure.

 b) Though the decoder will handle a wide range of input levels,
    it is best to sample the audio source at moderate to high
    levels. Slight clipping should not cause any problems.

 c) It is not necessary to specify the number of stop bits when
    decoding - unless the strict option (-X) has been selected.

 d) Decoding begins with the start bit found and continues until
    the end of the file or an error occurs. If there is more than
    one program present on a wavefile, the programs will be
    concatenated. The output file will contain program data in
    the form found on the tape. It may be viewed using the -C
    switch if desired.

 e) If an ill-formed bit is encountered, a "Bad pattern" error
    will be displayed. Any preceding valid data will be saved
    before the program exits. Pattern errors may result from a
    variety of causes e.g.

    - not 8-bit mono wavefile recorded at 22050 samples/sec.
    - not Kansas City Standard or CUTS data
    - serial format not correct (default settings allow either
      8N1 or 8N2 data to be decoded).
    - incorrect baud rate (default 300)
    - very low recording level
    - wavefile has very poor waveshape, excessive DC offset or
      phase shift

 f) DC offset, hysteresis and timing controls (-F -H -G)

    Wavefiles having a very poor waveshape may give rise to
    "bad pattern" errors. This can be due to head mis-
    alignment between the cassette record and playback
    devices. Such problems can sometimes be compensated for
    by the judicious use of the DC offset and hysteresis
    controls (-F -H). The default values are 0 and 3
    respectively.

    Speed difference between tape record and playback devices
    can also result in decoding failure. The timing control
    (-G) can be used to compensate. The default value is 0.

 g) Playback device

    If the tape playback device has any tone controls, these
    should be set for a 'flat' frequency response.

    Avoid portable cassette recorders of the "ghetto blaster"
    variety as these often have bass and treble boost which
    can introduce excessive phase shift and affect decoding.
    Experimenting with the tone or treble controls may help.

    A hi-fi stereo cassette deck should work well, but sample
    from one channel only.

2. Encoding

 a) When encoding, it is important to specify the correct number
    of stop bits otherwise the machine on which you wish to use
    the tape may have problems reading the data!

 b) The default tone used is a shaped square wave and results in
    an optimum waveform when played back from a cassette. A sine
    wave option is provided (-T switch) however it is likely to
    be less effective, particularly at the higher baud rates.

 c) It should not be necessary to use the waveform invert option
    (-I switch). Most computers should handle waveforms of either
    polarity.

 d) The encoded wavefile can be stored very effectively using
    any file archiving program such as PKZIP, ARJ, WinZIP etc.
    Archived wavefiles are typically 1% of their original size.

3. Baud rates higher than 300

   The Kansas City Standard specifies an operating speed of 300
   baud. A common modification by users was to increase the speed
   to 600 baud or higher. This was achieved by either doubling the
   tone frequency or halving the cycles per bit.

   The KCS utility can only decode/encode higher baud rates which
   use the latter method.

4. CUTS format

   The CUTS format was created by Processor Technology Corp.
   and was meant to be "upward compatible" with the Kansas City
   Standard. Many Processor Technology program tapes were
   recorded using 300 baud Kansas City Standard on one side and
   1200 baud CUTS on the other.

   Technically, the CUTS format is similar to the Kansas City
   Standard but uses a 1/2 cycle of 600 Hz to represent a '0' bit
   and 1 cycle of 1200Hz to represent a '1' bit.  The data rate
   is 1200 bits per second. The serial format is one start, 8
   data, two stop bits, no parity.

   An external utility SOLENT is available which will convert
   CUTS binary program files produced by KCS to text form
   suitable for loading into a PT computer or emulator.

5. Phase distortion issues

   All audio cassette players include 120 uS tape equalization
   during replay - a side effect of which is the creation of
   phase distortion. While this is inaudable to the ear, it can
   affect computer program data. To counter this, many computer
   cassette interfaces included phase precompensation in the
   audio output.

   Some computers did not include phase precompensation. The
   reason why this did not adversely affect performance was
   either 1) very low baud rate or 2) a phase-locked loop was
   used for decoding which is relatively insensitive to phase
   distortion anyway.

   A wavefile with phase distortion can sometimes be corrected
   sufficiently to allow decoding with KCS. To do this you
   need a wavefile editor that can apply low-pass or high-pass
   filtering (which one works will need to be determined by
   experiment). The filter frequency should be set to approx
   1KHz with a 6dB per octave roll-off.

   Note: The wavefiles produced by KCS are precompensated
   (square wave only) and therefore suitable for recording to
   cassette.

6. Minidisc, MP3 and other "lossy" audio formats

   These formats were intended for music and voice use only.
   Do not use them to compress or store computer data wavefiles!
   They use lossy compression methods which can introduce enough
   distortion to make subsequent decoding of program data
   impossible.

   Note: Wavefiles produced by KCS compress extremely well when
   archived using ZIP etc. Not only is there no loss of signal
   quality, the compression is far superior than that obtained
   by storing on Minidisc or as an MP3 wavefile.

7. Limitations

   KCS is not very tolerent to phase shift distortion and there
   may be occasions where some tapes which work fine on your
   computer simply won't decode using the utility. See section 5
   for further details.

8. References

   The decoding algorithm is derived from that found in Wouter Ras'
   ATOMTAPE utility. (www.homepages.hetnet.nl/~wouterras/atom.htm)

9. History

   0.4   Included Processor Technology CUTS tape format
   0.5   Fixed sine tone option for CUTS mode
   0.6   Re-organised interface. Many options have been changed
         and decoding is now the default mode. Added parity and
         7 bit data options.
   0.7   Decoder changed to give better results with marginal
         tapes. Added timing control.
   0.7b  Updated to DX-Forth 3.1 - no functional change
   0.8   Faster decoding. Add option to ignore decode errors.


