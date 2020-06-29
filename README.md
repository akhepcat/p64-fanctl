# p64-fanctl
bash script to control a small fan from a pine64 GPIO

usage: fanctl [start|stop|setup|on|off|auto|unauto]

For a 5v fan, you can use a simple 1-transistor interface like: http://elinux.org/RPi_GPIO_Interface_Circuits#Output_circuits

For a 12v fan, you'll need a 2-transistor design as alluded to on https://www.baldengineer.com/pwm-3-pin-pc-fan-arduino.html/npn-pnp-driver-low-1520px
however his pins may not be the same as your pins, so I've posted a clean schematic with a corrected, generic pin-out [12V-Fan-ctrl.png]  - you'll need to validate your transistor pins before wiring.

I use an 80ma 5v micro fan, which is compatible with the basic NPN
circuit, and only requires two extra parts. a 1k 1/4w resistor, and an
all-purpose NPN transistor (NPE123AP or equivalent)


auto mode will start the script up backgrounded in a screen session and
watch the system temperature until it exceeds the preset limit of 50c, at
which point the GPIO pin will swing high, and hopefully cause your fan to
run.   The fan should run for $((5 * $UPDATE)) seconds after the temperature
drops below 50c, in order to prevent a lot of on/off cycling, and to give
your heatsink some extra cooling love.


In the script, there are two variables that are useful to you:

\# which GPIO pin are you using  
GPIO=75


\# In auto mode, how often (in seconds) do we check for temperature changes?  
UPDATE=5
