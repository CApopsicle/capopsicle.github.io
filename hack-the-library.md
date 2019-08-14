---
layout: project
---

## HackTheLibrary 
#### NTU Library Studying Area Seat Arrangement System Reformation

This project is an elegant redesign and implementation of the library's seat arrangement system at National Taiwan University(NTU). Our interface aims to provide an intuitive way to choose seats in the studying area.

This Project is made and maintained by Hack Campus team, a group of NTU students who strive to change the campus by technologies.

![new interface](https://i.imgur.com/s26uxvk.png)
The new version interface


### The Early Design Research
### The Problem

The old selecting seat system and rules of studying area is a poor design. The whole process goes like this:

We had an old PC displaying seat numbers like an Excel spreadsheet. The students could look at an incomplete paper map on the wall, and then, they are required to select a seat in our system and sign in by his student ID at the entrance of studying area. Once entered the studying area, he could only sit at the position he picked. If someone wishes to change his seat, he must re-select a place on the system and scan his ID again. These rules are designed to prevent students from saving seats.​

However, many students did not follow these rules because re-selecting a seat on the system is very annoying. Moreover, if a student seats in the position that isn't assigned to him, it will affect the next person who chooses this position. Most of the affected students would not complain, and he might end up occupy another seat that isn't assigned to him, either. Therefore, one unruly behavior strikes like a propagation, and in the end, nobody is seating on the assigned seat.

To solve this problem, the Hack Campus team used the following design methods for the reformation. Visit here for a more detailed report.

![The old system](https://i.imgur.com/qaTGZAt.jpg)
The old system

### Interview and Affinity Diagram

We interviewed 6 students including light user to heavy user of the studying area, collecting their studying habits and selecting seat habits in the studying area. After the interviews, we used the Affinity Diagram to look for the patterns from our interview transcripts. We made assumptions according to the facts from the interviews:

- Most students use the studying area during midterms and finals.
- When students find out that the position they chose is occupied, they tend not to seek for the administrator's help because they don't want to disturb others, and they do not want to waste their own studying time.
- Students are too lazy to change seats on the system once they enter the studying area 
- There are some students care about where they sit a lot, and they tend to sit at some certain positions they like.
- The primary disturbance in the studying area is because of people moving around for changing seats, filling their water bottle, going to restroom, etc. The secondary disturbance is about the environment: whether there are others sitting next to me, whether there is a strange person, and whether is a beautiful girl.


### Ideations after brainstorming

1. Register a seat after searching an ideal seat in the studying room.
2. Read a detailed floor plan of the studying room at the entrance to assist seat-selecting before entering.

### Questionnaire

To verify our assumptions, we designed a questionnaire and sent it to all students in the university. We collected 758 valid questionnaires in the end.​

![The Questionnaire](https://i.imgur.com/IAmSuvM.jpg)
The questionnaire

### The Facts

- 47% of the user study at the studying area on only midterms and finals. (Let's define them as light user)

- The top 3 information users want to know from a selecting seat system are:
1. How many people are sitting at the same table?
2. Is this seat allowed to use computer?
3. Is this seat clean?

- The current system can not provide sufficient information about the seats for the users. 47% of them will not sit at the position they selected before they entered.
- 33% of the light user can not distinguish which area in the studying area is allowed to use laptop.
- If selected a seat but it is occupied by the other, 73% of the user will not ask the other student to leave, instead, they will switch to an empty position.

### Feedbacks on the ideations

74% chose the first one: registering a seat after searching an ideal seat in the studying room, and 26% chose the second one: reading a detailed floor plan of the studying room at the entrance to assist seat-selecting before entering.

![Ideation1](https://i.imgur.com/5eWNmyV.jpg)

![Ideation2](https://i.imgur.com/OBOYsAw.jpg)

### Our design

![Design1](https://i.imgur.com/85LhVPm.jpg)

![Design2](https://i.imgur.com/OjBwGRE.png)
Filters of the map: select the filters and the map will respond with the seats corresponds to the filters by changing the opacity.

![Design3](https://i.imgur.com/HloSjHE.png)
Panel for displaying last-time seat and recent seats after the a student scan his student ID card.

![Design4](https://i.imgur.com/QWNXsal.png)
The map view: (1) The map view replaces the spreadsheet-like interface, showing detailed floor plan and spatial information. (2) Use colors to represent status of the seats. Green is available, yellow is temporarily leave, and red means the seat is currently being used. (3) The SVG map enables zoom in and zoom out by the button or the scroller of the mouse.

### Implementation

Built with...

- Angular.js 1 - web framework
- MongoDB - database
- Gulp, Bower - packaging, building, development tool
- D3 - SVG interaction