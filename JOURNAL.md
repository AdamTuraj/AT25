---
title: "AT25"
author: "Adam Turaj"
description: "A GT3 inspired RC car"
created_at: "2025-06-16"
---

# AT25 Journal

This journal will document my findings and progress throughout the project.

## Day 1 (June 19th)

**Time Spent**: 3

**Total Time on Project**: 3

---

Day 1 involved researching and selecting the necessary components. I plan to order most of the parts from GreatHobbies, a Canadian hobby store.

Initially, I selected the battery based on my preferred voltage of 7.4V due to the availability of batteries and motors, and it being at an ideal performance range. For the capacity, I opted for 5000mAh to achieve a decent runtime while remaining cost-effective.

Next, I chose the motor, which required thorough research and consideration. After evaluating the options, I decideed that using a single motor for a RWD setup would offer better cost-effectiveness and performance than 2 motor AWD. The selected motor is a 1406-2280KV, 4-pole sensored model, which can be found in the Bill of Materials (BOM).

Lastly, I selected the tires. Although I originally wanted RC slick tires, the best available option was vintage racing tires. I chose a 26mm width for the front tires and a wider 31mm for the rear.

The BOM can be found at the following link: [AT25 BOM](https://docs.google.com/spreadsheets/d/1flXe85N5WV3nN8ESYz18NZuvuu6GO_V06G4YLhqS2Ls/edit?usp=sharing)

![The BOM](https://hc-cdn.hel1.your-objectstorage.com/s/v3/34b6dca96e3978a9ee3a535140ec9d82047ec993_image.png)

## Day 2 (June 20th)

**Time Spent**: 2

**Total Time on Project**: 5

---

Today, I began laying out the general design of the car. I began by learning how the aerodynamic elements work and the different elements used. Through this, I got refreshed on Bernoulli's and got a surface level understanding on how the important elements work.

Knowing this, I made a rough sketch on paper as a guideline on how I will design the car. This rough work can be found below.

Finally, I made and found the 3D models for the components I will be using. My plan is to design the aero then determine the packaging for everything else, a similar process used in F1 and other design teams.

Note: I changed the battery to a different, similar spec'd one due to a proprietary connector.

![The rough sketch of the RC car](https://hc-cdn.hel1.your-objectstorage.com/s/v3/385cd5cd533fd6cc2addcd017ffad2ef2bab02a1_img_8022.jpeg)

## Day 3 (June 21st)

**Time Spent**: 5

**Total Time on Project**: 10

---

In Day 3, I began work on the brushless control board. The IC pre-driver I selected was the DRV8323S due to its 1 PWM mode (no extra code required), my previous experience with it, and its availability.

I preferably would run the DRV8320S but it is out of stock so I had to compromise. This IC would be better as it doesn't include the amplifiers which are not required due to the sensored motors not needing to know the current flowing through the coils.

Afterwards, I chose the CSD87333Q3D FETs as it is TI (I love Texas Instruments), it integrates both the high and low MOSFETs, supports up to 15A (the limit I'm designing for), and the high efficiency while being cheap and available.

Drawing the schematic mainly involved following the diagrams provided by TI. It was very straightforward; however, the PCB layout will not.

The final schematic for the board is this:

![Final Schematic](https://hc-cdn.hel1.your-objectstorage.com/s/v3/8eae5faa91f8c98d03fa222825bc17d268089a94_image.png)

## Day 4 (June 22nd)

**Time Spent**: 3

**Total Time on Project**: 13

---

I did some more research while looking for footprints and came to the following conclusions:

- I will be attempting to assemble the boards myself again
- Bulk capacitor banks are required
- The DRV8320RS is preferred for my application as:
  - I do not need the current sense amplifiers (I'm using a sensored motor)
  - The buck converter is necessary for my application

Regarding conclusion #1, I will be assembling them myself due to the high costs of JLCPCB assembly, and my previous experience assembling SMD boards. I had issues assembling my last board which is the reason I was planning on using PCBA; however, I made the realization that my solder paste is expired which I believe is the source of the problems.

After making these conclusions, I adjusted my schematic to reflect them. This included updating the DRV footprint (although I haven't changed the pinout from the DRV8323RS -> DRV8320RS). The capacitance of the bulk bank was stolen from an existing open source design.

I started adding the circuitry around the buck converter but still need to fill in the values. Below is my plan on how the board will be powered:
![Flow chart of power circuity](https://hc-cdn.hel1.your-objectstorage.com/s/v3/aa759014652247c120b7a52cfe677ecdad9f329c_image.png)

And here is the current revision of the schematic:
![Current Schematic](https://hc-cdn.hel1.your-objectstorage.com/s/v3/61036e09d5d0d80cc4c21ae81d8042cd64b4b91d_image.png)

## Day 5 (June 27th)

**Time Spent**: 7

**Total Time on Project**: 19

---

Throughout today, I tweaked the schematic, picked parts, and designed the layout.

Firstly, I made the following changes to the schematic:

- Added a RC filter to the hall effect sensors
- Adjusted the symbol to the DRV8320RS
- Finished buck converter circuitry
- Change 10uF bulk capacitor to 100uF electrolyte capacitor
- Added 0.1uF capacitors to each gate
- Cosmetic adjustments

These changes resulted in the final, completed schematic:
![Completed schematic](https://hc-cdn.hel1.your-objectstorage.com/s/v3/a2eccc6b94371e0a6ef36dab957d2c63444db661_motor_driver.png)

Afterwards, I assigned footprints and picked part numbers. With all that done, I layed them out, and carefully wired them up. Due to the relatively high current and to simplify wiring, a 4 layer board was a no brainer. The stackup I used, as I have done with all my other 4 layer boards, is:

- Sig / GND
- GND
- PWR
- Sig / GND

For the first time ever, I made the entire board without a single DRC error: no clearence violations, missed connections, etc!

Below is the final design for the ESC:
![3D view of PCB](https://hc-cdn.hel1.your-objectstorage.com/s/v3/026301dc0eeec364d06b7de6c3771141921c3320_image.png)
![PCB Layout](https://hc-cdn.hel1.your-objectstorage.com/s/v3/e2a30e74069a72bd700e183be4fe7425fea80c3d_image.png)
