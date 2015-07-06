# GUI\_Test\_Hand #

The ''GUI\_Test\_Hand'' was created to test the motors of the i-limb (or any other hand using DC motors), and manually change the duty cycle of the pulse width modulation (PWM). Each finger can be moved in both directions.

NOTE: This function doesn't use the object-oriented [Movements\_Protocol](Movements_Protocol.md). Please see the [GUI\_TestPatRec\_Mov2Mov](GUI_TestPatRec_Mov2Mov.md) for reference in working with the movement and motors in the object-oriented way.

The GUI consists of 2 main parts:

## Initialize the serial connection ##
> There are 3 buttons (''Connect, Disconnect, Test connection'') which handles the communication
  * Connect: Calls "Connect\_ALC" which returns the communication object saved in the  handles as "com". The "com" object is necessary for all future   communication.
  * Test Connection: Calls "TestConnectionALC" which writes a 'C' and expects a 1 in return if the communication is successful.
  * Disconnect:  Close the 'com' object.


## Control ##

  * Speed and Length:
> The ''speed'' is proportional to the duty cycle.
> The ''length'' is related to the time the movement will be activated

  * Finger control
> Each finger can be opened and closed  with the referring pushbutton. The function ''Update2PWMusingSCI(obj, pwmID, pwm1, pwm2)'' is executed with different IDs per finger. The function gets the object from handles.com and the pwmID for the motors of each finger (A=thumb,...E=little finger). PWM1 and PWM2 define the directions movement. One of them must be 0 and the other is the value imported from the GUI (speed)). This is because the motor driver required two PWMs.

> The functions of the buttons can be inversed by activating the checkbox for the particular finger.