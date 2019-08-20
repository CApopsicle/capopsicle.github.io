---
layout: project
---

## Wash-N-Watch
#### The Girl’s dorm washing machine monitoring and notifying system

### The Problem
University dorms are not an ideal place for living, there are no private bedrooms, the insulation is pretty bad, and there's a limited amount of house appliances. In NTU girl's dorm, we had 100 girls using only 2 washing machines. Washing clothes is a painful experience. 

From this user pain point, comes this project of designing and implementation of a monitoring system for washing machines in NTU girl's dorm. Our system aims to display the status of every washing machine in the girl's dorm. We enabled **sign-in**, **subscription**, and **text message notification** for users. A user of our service can subscribe to a certain washing machine on our webpage, and she can get a text notification when that machine finishes its washing schedule.

![image1](https://i.imgur.com/BOvNdWa.png)
The interface of home page showing the two washing machines and their status

### Scenario
Amy is in her junior year at NTU, and she lives in the girl's 1st dormitory. She wants to do her laundry on a Saturday morning. However, the 2 washing machines on the 2nd floor are currently being used. One of them will finish washing in 30 minutes, and the other in 15 minutes. Amy takes the heavy laundry back to her room. However, when she goes again to the laundry room 20 minutes later, the machine is being used by another new user, and Amy has to keep on waiting. In addition, there's a big pile of washed clothes sitting on top of a washing machine, and some of them are scattered on the floor. These are the clothes of the previous user, and they are taken out and piled up by the new user. Amy feels sorry for that previous user because her clothes are now dirty again. Yet, if Amy wants to wash her clothes in a hurry and the previous user's clothes occupy the washing machine, she may do the same thing.

![image2](https://i.imgur.com/aBOAdqf.jpg)
The laundry room with a pile of clothes on top of a washing machine

From our personal experiences and talking to several of the residents, we had several problems with our washing clothes process

- There are too many students for only 2 washing machines.  During the busy hours, it's hard to get access to a washing machine.
- The remaining time displayed on the machine is inaccurate.
- People forget to pick up their clothes when they are done.

### Design Alternatives
### System to detect vibrations
The first approach we had was using sensors that detect vibrations in the washing machine with Arduino. However, the sensors we had were too sensitive. Therefore, they could not differentiate between subtle and excessive vibrations.

![image3](https://i.imgur.com/997jZ2e.jpg)

### Monitoring electrical energy
We tried to look for other quantifiable data that discriminate between the different washing machine statuses (**water-in**, **rinsing**, **water-out**, **spinning**). After several trial and errors, we found that the electrical energy varies between these statuses.

![image4](https://i.imgur.com/XdAnbnT.jpg)
Variation of electrical energy in the different states

We then found a smart home appliance that corresponds to our needs. It was a smart plug made for monitoring power consumptions, and it provides data on the electrical energy consumed. We contacted the company of this smart plug and proposed our ideas to potentially collaborate with them.

![image5](https://i.imgur.com/edvYfNf.jpg)
The architecture of our system

To distinguish between the states based on the energy consumption, we used machine learning to train a decision tree model to predict the current progress and status synchronously. We collected 3-day electrical energy data from girl's dorm laundry room (2 machines) as our training data and ran our model.

However, our model had low precision because there was irregular usage of the washing machine. For example, users keep opening the lid of the washing machine to add more clothes, or sometimes the electric power gets tripped. To fix this, we stored the last active stage value (water-in, rinsing, water-out, spinning) of the last minute since minute is our time unit. This gave us a much higher accuracy.

### Interface Design
In the main panel of our interface, we listed all the washing machines with their status, progress bar (in %) and the overall washing schedule. By logging in and clicking on the subscribe button of a certain machine, the user will get a text message when the current washing schedule is complete.

![image6](https://i.imgur.com/I4F6tov.jpg)
Home page showing the status of the available washing machines

![image7](https://i.imgur.com/INMI6kc.jpg)
Screenshots of our mobile web app and text message notification of an anonymous​ user

The system is built with
- Angular.js 1 - web framework
- MySQL - database
- Gulp, Bower - packaging, building, development tool
- Node.js, Express.js - backend services: subscription, sign-in/log-in
- Twilio - text message service

### User Feedback
![image8](https://i.imgur.com/B1CAnbZ.jpg)

We pinned up a QR code for residents to download and use our app with a line explaining the application on the whiteboard and asked them to leave their feedback. Some feedback we received were:

> Oh this is so amazing
>
> Can you build this for the third floor too?

[Back](./)