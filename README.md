# Interactive-SIRmodel-UI

An interactive program to visualize the influence of certain parameters on herd immunity. The used basic underlying mathematical model is the SIR-model. 

The upper plot shows the percentages of Infected people over time. For the plot below, the user can select to either plot the percentage of immune people (I+R), or the reproduction rate R over time. The R-value was calculated according to the following equation, with R0=beta/gamma, pC = reduction in transmission rates from safety measures, pI = reduction of transmission rates from virus immunities.

```math
R = (1-pC)*(1-pI)*R0
```

The model contains N=1000 individuals in the population. The initial values of S, I and R at t=1 are S0=999, I0=1, and R=0. Up to 4 models can be plotted simultaneously.


# Controls
  
User input | Description
--- | ---   
Left-/Right-/Up-/Down-keys | Navigating through the parameters
Left-/Right-keys | If a parameter was selected: Increasing/decreasing its value
X-key | Selecting/ Deselecting a parameter
R-key | Switching the plot below to either: <br/> • Show percentage of immune people <br/> • Show R-value over time
C-/E-/M-/P-keys | Set preset variables for COVID-19, Ebola, Measles or Polio respectively


  
  


# Parameters of the program
By changing the parameters, the user can adjust/extend the classical SIR-model. 

Parameter name | Description 
--- | --- 
Show plot? | Boolean parameter that switches the visualization of plots on/off.
beta | Average number of infections that one person causes per timestep.
gamma | Inverse of the average time that one person stays infected.
Lockdown? | Boolean parameter that controls whether or not a lockdown is present.<sup>1,2</sup>
L_start | Start date of lockdown (unit: days)
L_duration | Duration of lockdown (unit: days)
L_redRate | Reduction rate of contacts during lockdown (1: No reduction, 0: Strict lockdown with zero contacts)
P_Type? | Describes the type of population.<sup>1</sup> Can have 3 different values:<br/> • Homogen: Homogeneous population <br/> • Gamma<sup>2</sup>: heterogeneous population according to [.....] <br/> • Matrix<sup>2</sup>: Heterogeneous population according to [….]
P_H_var | Additional parameter that are used for the population heterogeneity models. <br/> • “Gamma”: Todo: ?? <br/> • “Matrix”: Parameter used by SEIR-model. (Inverse of the incubation period of the disease)

<sup>1</sup> Lockdown?=False and P_Type?=”Homogen” correspond to the classical SIR-model. <br/>
<sup>2</sup> See "extensions of SIR-model" below



# Extensions of classical SIR-model

### Lockdown

Lockdown restrictions influence the parameter beta, as it describes the average number of infections that one person causes per timestep.
We denote the new average number of infections that one person causes per timestep during lockdown as Li, with Li=Lockdown intensity. It is therefore:
- Li= 1: no lockdown, 
- Li= 0: Strict lockdown during which every person has zero contacts

We can then split the course of time t=[1:200] into 3 time regions ("before lockdown", "during lockdown", "after lockdown") and model each region by its own SIR-model. If without restrictions, one person infects b other people per day, the 3 SIR-models then correspond to:
1st SIR model: Course of the pandemic until the lockdown (with beta=b)
2nd SIR model: Course of the pandemic during the lockdown (with beta=b*Li)
3rd SIR model: Course of the pandemic after lockdown (with beta=b)

### Population heterogenity "Matrix"

This extension is based on the paper by Britton et al. (2020).

Here a SEIR Model is used, which considers an additional exposed population. Exposed individuals are not infectious during the incubation period of the disease. 
We consider six different age groups with different transmission rates with respect to each of these six groups. This builds a 6x6 contact matrix beta. The P_H_var and gamma values, which are the inverse of the incubation and infectious period respectively, are assumed to be constant for these six age groups. 

We start with one individual being exposed at time t=0 and the rest of the population being susceptible. The removed and infected population at time t=0 is zero. The S,E,I and R values are solved from the differential equations for each of these 6 age groups, which yields 4x6=24 values. The S, E, I and R values of the total population are calculated by adding the array of values corresponding to each age group. 

The initial behaviour of the infected population depends on which of the six age groups is exposed first.  The curve of the infected population might show a small initial peak. This behaviour of the model is because the first individual gets infected after the incubation period of the disease and this same individual joins the group of the removed population R while the next set of individuals, who got exposed, are still in their incubation period.

### Population heterogenity "Gamma"
This extension is based on the paper by Neipel et al. (2020).

-TODO: descriptions-


# Credits
- **Gamma-extension**: Moritz Schramm
- **Basic SIR-model, Matrix-extension**: Tom Richard Vargis
- **Pygame-UI-interface, implementation of lockown-measurements, icon.png**: Marie Langer
- **Font**: TYPEW.ttf by Johan Holmdahl

DISCLAIMER REGARDING FONT USAGE:

*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*

 Type wheel

  This truetype typewriter font was borned at
  Free Typewriter Fonts
  http://www.free-typewriter-fonts.com

  You may distribute, sell, resell, change
  or modify the font - and you are allowed to upload
  the font onto any site or CD if this disclaimer is
  included in the download (text.txt).

  Any other means prohibited.

  Johan Holmdahl
  info@free-typewriter-fonts.com

  April 2001
  
 
*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*

# Bug report

If you encounter any bugs, please send a mail to marie.langer@mailbox.tu-dresden.de



