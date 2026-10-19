# Introduction
The idea of power electronics is to control and convert Electricity
![[Pasted image 20261015202450.png]]

In the past power electronics is for very high voltages but now it is also for things in milli voltage
![[Pasted image 20261015202809.png]]

What is really in power electronics system
![[Pasted image 20261015203201.png]]

## Why we need power electronics ?
Why we need a power electronics, we can convert from voltages in very easy way (voltage drop in the resistor)
![[Pasted image 20261015204134.png]]

But the problem of it is the efficiency so for the the "**Liner Regulators**" not recommended
n = Pout/Pin = Vout x Iout / Vin x Iin = Vout / Vin = 5/15 !!!

## Switching Convertors
The idea here is to to make voltage switching very speed and use the average voltage for it
![[Pasted image 20261015205002.png]]

The switching from transistor and the average from law pass filter (inductor stable the charge and capacitor move AC to ground)
and the efficiency up to 1% and the idea of that is the power drop in switch is zero (if it ideal no resistance for it) + the inductor and capacitor are store elements so there is no dissipate for it 

So the output voltage is depend on the switching frequence

# Analysis Methods and Rectifiers

![[Pasted image 20261015211910.png]]
The diode is not controlled

![[Pasted image 20261015211835.png]]

## PSS (stady state)

![[Pasted image 20261015212144.png]]

The average value of V in inductor is 0 in PSS
The average value of I in capacitor is 0 in PSS
![[Pasted image 20261015212458.png|283]]


## when u use diode and inductor
what happens here is the inductor store the energy and when the diode is **want** to to OFF the inductor move the current (lagging) so the diode continue ON and pass the negative wave of voltage 
**"The diode don't care about voltage it care about current direction"** 
![[Pasted image 20261015213445.png]]

and the solving of the negative voltage is to use another diode 
![[Pasted image 20261015213543.png]]

![[Pasted image 20261015213849.png]]

# Load Regulation

![[Pasted image 20261015215638.png]]

Now in the really live we see this 
![[Pasted image 20261015220700.png]]
The L1 is from wires (not a component we put it) so it is a small inductor