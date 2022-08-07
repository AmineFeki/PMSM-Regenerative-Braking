# PMSM-Regenerative-Braking

This project follows the PMSM-Speed-Torque-Control that I have already pushed to my account.

Braking a PMSM is one of the most important applications that we need them in Electric Vehicles and Electro-mobility.

Let's go! 

# 1- Mechanical braking:

It is a contact method. It consists of augmenting the friction coefficient which applies a resistive torque and make the rotor stopped.

![image](https://user-images.githubusercontent.com/53936812/183287877-6f1635fc-6725-4b52-8b57-11d2e7d48672.png)

In this case, the kinetic energy will dissipate by Joule effect.

==> The mechanical option is not always the best solution.

# 2- DC injection braking:

It is a non-contact method. It consists of applying a fixed DC to the motor stator windings. When the fixed DC is applied, the rotor quits chasing a rotating magnetic field and tries to align itself with the fixed magnetic field produced by the fixed DC. This method decelerates the rotor speed progressively, till the rotor stops.

![image](https://user-images.githubusercontent.com/53936812/183287896-e98b59e6-0427-4689-8d77-bfe7c3f2d21d.png)

This method has the advantage of not being mechanical. But again, the kinetic energy will dissipate, and this method consumes energy to stop the rotor.

==> It does not represent the most suitable solution.

# 3- Dynamic braking:
## a- Using braking resistors:

It is a non-contact method. It consists of shunting the windings with external resistors. The windings inductances discharge in the braking resistors.

![image](https://user-images.githubusercontent.com/53936812/183287915-847934fa-2fd5-48e9-a5eb-82944d12fe25.png)

This method is more interesting than the previous others. It does not consume energy to stop the motor and it is not a mechanical one.

A simple view on the energetic balance sheet, we can easily constate that the kinetic energy is again dissipated by Joule effect. We would like to be more efficient and explore this energy. And here comes the regenerative braking method.

## b- Regenerative braking:

As mentioned before, this method allows us to explore the kinetic energy.

We all know that the PMSM and the motors in general could work as generators in some conditions.

![image](https://user-images.githubusercontent.com/53936812/183287930-054eac04-83aa-447a-bbfe-8a1e2ee5f89b.png)


A motor can work in two different modes:

• Motor: P = U.I = Γ.Ω > 0 (First and third quadrants)

• Generator: P = U.I = Γ.Ω < 0 (Second and fourth quadrants)

In the chapter of the regenerative braking, we focus on the generator mode, and particularly the quadrant in red. (The speed is supposed positive)

The idea here is to either to regulate velocity to follower a ramp guide and progressively reach zero or obtain the minus iq proportional to the requested brake torque.

Let’s study the option of generating a negative torque!

According to Article 1, our goal is to make the consumed power from the power supply Pin=0. It implies that:

o 𝑖𝑞= −(0.375.𝑝.𝜑𝑃𝑀𝑅𝑠)𝜔𝑒𝑙𝑒𝑐 and 𝑇𝑑𝑒𝑣= −(0.28125.𝑝2.𝜑𝑃𝑀2𝑅𝑠)𝜔𝑒𝑙𝑒𝑐

o 𝑖𝑑=0

where: 

Iq: The current component on the q-axis

Id: The current component on the d-axis

P: Pole pairs number

𝜑𝑃𝑀: The Permanent Magnet Flux

Rs: The per-phase resistor

𝜔𝑒𝑙𝑒𝑐=2𝜋𝑓𝑒𝑙𝑒𝑐: The electric pulse

This value ensures the maximum amount of current recovery.

What about the Maximum Energy Recovery Switching Scheme (MERSS) for regenerative braking?

### Maximum Energy Recovery Switching Scheme (MERSS):

As mentioned before, in the regenerative braking phase the motor acts as a generator based on the B-EMF. The B-EMF is generated thanks to its kinetic energy and the inverter switches to a boost converter (It converts DC voltage to a DC one).

During the braking phase, the PWM signals applied to the MOSFETs gates are still there. In on period, there are two cycles:

o The ON-Time:

During this time, the motor is free-wheeled and generated current (thanks to the kinetic energy of the motor) is dissipated.

In this phase, no energy is recovered.
![image](https://user-images.githubusercontent.com/53936812/183287987-6ff8a050-5edb-4ad9-898b-8dd87f800678.png)

Here all the HIGH MOSFETs and S4 are disabled and S2 and S6 are enabled.

The current pass in a backward way through S2 and S6 and in a positive way through the freewheeling Diode of S4. 

𝑖𝑚𝑜𝑡𝑜𝑟≠ 𝑖𝐷𝐶

o The OFF-Time:
During this time, the motor is generating a backward current that is, thanks to the combination of inverter’s switches, driven to the DC-supply that absorbs it.

In this phase, the electric energy generated from the motor (due to its kinetic energy) is recovered by the DC-supply.

![image](https://user-images.githubusercontent.com/53936812/183288003-570a7d41-2b0d-45c2-b708-a0d90bd75f07.png)

Here all the MOSFETs are disabled and the freewheeling Diodes of S1, S4 and S3 and enabled. The current is driven from two motor phases to the DC-supply and returns from the third phase.
