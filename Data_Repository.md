This folder contains a repository of myoelectric recording sessions ([recSession](recSession.md)) useful for development, as well as for algorithms benchmarking on common data sets.

Remember that even if you are using the same data to compare different algorithms, small variations in signal processing and training settings can make a difference on the final results.

The recording session described below can be download from [Source Code](SourceCode.md)

## 10mov4chUntargetedForearm ##
  * 10 hand and wrist motions
    * Hand Open/Close
    * Wrist Flex/Extend
    * Pro/Supination
    * Fine/Side Grip
    * Pointer (index extension)
    * Agree or Thumb up
  * 3 seconds contraction time with 3 seconds for relaxation between each repetition
  * 3 repetitions of each motion
  * 4 bipolar electrodes (Disposable Ag/AgCl)
  * 1 cm electrode diameter
  * 2 cm inter-electrode distance for the bipole
  * Electrodes were equally spaced around the most proximal third of the forearm.
  * The first channel was always placed along the extensor carpi ulnaris
  * The proximal electrode of each bipole was always connected to the positive terminal of the BioAmp.
  * 17 subjects ([original study](http://www.scfbm.org/content/8/1/11))
  * 20 subjects (final release)
  * Amplifiers:
    * In-house design (MyoAmpF2F4-VGI8)
    * CMRR > 130 dB
    * Gain 71 dB
    * Embedded active ﬁltering:
      * 4th order high-pass ﬁlter at 20 Hz
      * 2nd order low-pass ﬁlter at 400 Hz
      * Notch ﬁlter at 50 Hz.
    * Galvanic isolation rated to 1,500 Vrms
  * Signals were digitized at 2 kHz with a 14-bits resolution.

## 6mov8chUFS (Untargeted Forearm Simultaneous) ##
  * 27 clases
    * 6 Individual hand and wrist motions
      * Hand Open/Close
      * Wrist Flex/Extend
      * Pro/Supination
    * 20 possible combinations of the motions above
    * 1 no motion / rest class
  * 3 seconds contraction time with 3 seconds for relaxation between each repetition
  * 3 repetitions of each motion
  * 8 bipolar electrodes (Disposable Ag/AgCl)
  * 1 cm electrode diameter
  * 2 cm inter-electrode distance for the bipole
  * Electrodes were equally spaced around the most proximal third of the forearm.
  * The first channel was always placed along the extensor carpi ulnaris
  * The proximal electrode of each bipole was always connected to the positive terminal of the BioAmp.
  * 17 subjects ([published study](http://ieeexplore.ieee.org/xpl/articleDetails.jsp?arnumber=6744619))
  * Amplifiers:
    * In-house design (MyoAmpF2F4-VGI8)
    * CMRR > 130 dB
    * Gain 66 dB (2,000 linear)
    * Embedded active ﬁltering:
      * 4th order high-pass ﬁlter at 20 Hz
      * 2nd order low-pass ﬁlter at 400 Hz
      * Notch ﬁlter at 50 Hz.
    * Galvanic isolation rated to 1,500 Vrms
  * Signals were digitized at 2 kHz with a 16-bits resolution.