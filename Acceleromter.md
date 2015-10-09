NOTE: This is an ongoing development and therefore the documentation is not yet finalized.

# Accelerometer data #

BioPatRec only supports EMG data. However the [Delsys Trigno Wireless System](DTWS.md) includes a accelerometer in addition to the EMG. In order to store this data a new variable must be added to [recSession](recSession.md). tdata is the variable under [recSession](recSession.md) that contains the EMG data. It is three dimensional with the dimensions given by samples, channels and movements.

Acceleration data should however be structured differently, as there are three acceleration channels (x,y and z) on each sensor unit. To better separate the data from different axes a 4 dimensional structure is suggested.

adata is a 4 dimensional variable containing accelerometer data. The dimensions are given by samples, axes, sensors and movements. The new suggested structure for [recSession](recSession.md) wil be:

  * sF (sampling frequency)
  * sT (sampling time)
  * cT (contraction time)
  * rT (relaxation time)
  * nM (number of movements)
  * nR (number of repetitions)
  * dev (device used for the recordings)
  * nCh (number of channels)
  * mov (description of the movements performed)
  * date
  * cmt (comments)
  * tdata (total EMG data, Samples x Channels x Movements)
  * adata (total accelerometer data, Samples x Axes x Sensors x Movements)

With this structure there will be support for storing accelerometer data in BioPatRec. However There are currently no handles for these data samples.