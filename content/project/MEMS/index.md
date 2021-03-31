---
title: MEMS-based Flowmeter using an Ionic Polymer-Metal Composite Sensor
summary: Designed a small-scale vortex flowmeter with an interior diameter of 10 mm and implemented a 5 mm rectangular IPMC sensor to detect the frequency of vortices shedding from a bluff body. SLA printed and wired fully functional prototype. Performed COMSOL fluidstructure analysis to verify acquired experimental data. 
tags:
- IPMC
- Sensing
- COMSOL
- Modeling
- CAD
date: "2020-11-25T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption:
  focal_point: Smart

links:
- icon: microscope
  icon_pack: fas
  name: AMSL
  url: https://www.kwangjinkim.org/
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---
## Design Concept

- The proposed MEMS-based vortex flowmeter can be used in small- scale applications that necessitates devices with low power requirements.
- Ideally, the goal is to construct a small flow meter device (10 mm diameter) with the principle sensor being comprised of the electroactive polymer, an ionic polymer metal composite. IPMCs demonstrate sensing capabilities with heightened sensitivity.
- A successful attempt at this scale could demonstrate the feasibility of using this type of flow sensor in even smaller scale devices.

## Mechanism of Typical Vortex Flow Meter

A standard vortex flow meter operates based on the fluid phenomenon known as Karman Vortex Streets.
When flow is disrupted by an obstruction object or bluff body, vortices are shed from the object which is correlated to the following relationship known as the Strouhal number:

![Equation](https://latex.codecogs.com/svg.latex?St%20=%20fL/U)

where, 𝑓 is the frequency of vortex shedding, L is the characteristic length or hydraulic diameter of the object, and U is the flow velocity.

This relationship can then be related to Reynolds number where under a large Reynolds number range, Strouhal number is approximately 0.20.

A sensor can thus detect the frequency of the shed vortices, which is directly proportional to the flow velocity.

![MEMS](/static/media/MEMS_Images/MEMS1.PNG)
![MEMS](/static/media/MEMS_Images/MEMS2.PNG)

From Shanghai Yinuo Instrument Co. (Left) Cross section illustration of flow disruption in a pipe, generating vortices. (Right) Typical large vortex flow meter device.  

![MEMS](/static/media/MEMS_Images/MEMS3.jpg)

Strouhal Number as a function of Reynolds Number. Image from Thermopedia

## Advantages and Disadvantages

### Advantages

- Silent in use
- No moving parts
  - Less degradation
- Flexible usage range
  - 100 < Re < 200,000
- Low Power Requirements
- IPMC sensitivity can sense mild displacements that will occur from shed vortices
  
### Disadvantages

- Requires analysis within the frequency domain to acquire velocity
- Flow must be continuous for measurement (no pulsating flow)

## Concept and Prototype Design

### Initial Version

![MEMS](/static/media/MEMS_Images/MEMS4.PNG)
![MEMS](/static/media/MEMS_Images/MEMS5.PNG)

### Subsequent and Final Version

![MEMS](/static/media/MEMS_Images/MEMS6.PNG)

Failed and Completed Prints

![MEMS](/static/media/MEMS_Images/MEMS7.PNG)

## Physics Model - Visualization and Anticipation of Vortex Shedding

- A physics-based model was developed in COMSOL Multiphysics.
- Laminar flow physics was applied to a geometry resembling the cross-sectional area of the flowmeter device.

![MEMS](https://i.gyazo.com/0e91a2d53774171989e874033694cc85.gif)

Water at room temperature was set as the material and the normal inflow velocity was set to 0.07 m/s after an initialization step which was implemented to help the model run

![Equation](https://latex.codecogs.com/svg.latex?\rho_w%20=%20997%20[kg/m^3])

![Equation](https://latex.codecogs.com/svg.latex?\mu%20=%208.90%20\times%2010^-4%20[Pa-s])

![Equation](/static/media/MEMS_Images/Step.svg)

Using the Reynolds number equation, this puts us at a Reynolds number of about 235.

![MEMS](https://i.gyazo.com/bf9f913d2066575e498155969682bd62.gif)

## Experimental Setup

  ![MEMS](https://i.gyazo.com/a41b37e0e7597b4f8e675c9631e64772.gif)

- A contact piece was designed and soldered to read the IPMC signal.
- A Masterflex L/S series peristaltic pump was used to control the flow rate of the flowmeter.
  - The flow rate was calibrated to the specific hosing used.

![Equation](https://latex.codecogs.com/svg.latex?Q_e=5900%20[mm^3/s])

![Equation](https://latex.codecogs.com/svg.latex?V_e=0.075%20[m/s])

- Which results in a Reynolds number of 252, and thus an expected vortex shedding frequency of 4.76

![MEMS](/static/media/MEMS_Images/MEMS8.PNG)

## Results

![MEMS](/static/media/MEMS_Images/MEMS9.PNG)

- We can see the IPMC sensing the flow of the peristaltic pump in the following voltage reading plot.
- An FFT was performed on 2 of the 3 runs.
- Interestingly enough, we observe a noticeable frequency peak at around 4.7-5.0 Hz.
- However, it is important to note, this coincidentally is also the peristaltic pump pulse frequency as well.

![MEMS](/static/media/MEMS_Images/MEMS10.PNG)

## Conclusion/Future Work

- More experiments will have to be performed to validate the concept of the this design.
- Possible improvements:
  - A pulse dampener can be implemented into the setup
  - Redesigning the flowmeter
    - Better access to main chamber
    - Less clunky contact design
    - Further miniaturization
