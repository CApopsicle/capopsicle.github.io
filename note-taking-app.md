---
layout: project
---

## Integrating Non-Dominant Hand and Stylus Interactions for Tablet Note-Taking Applications

See our final report [here](./report.pdf)

### Introduction

Note-taking tablet applications are particularly popular for students and those in the workforce. Current note-taking applications on tablets follow a similar standard layout: **a static toolbar on one edge of the application and an empty canvas centered on the screen to write on. This layout has limitations that hinder productivity and take up valuable screen space.**

From previous research, it was found that a person that uses stylus and touch together for tablet-writing is ranked the highest by users in terms of their overall preference, ease of use, and accuracy compared to just pen or just touch inputs. Combining touch and pen balances the pros and cons of each; for example, the single input point of the pen is balanced by the multi-touch abilities of the hand, the pen's high precision can be blended well with the natural feel of a less precise touch, and more. This project combined the use of a stylus with the non-dominant hand to encourage this kind of interaction. **Specifically, this project focused on integrating the use of the non-dominant hand in note-taking applications in a way that does not disrupt the user and frees valuable screen space when desired.** Currently, the non-dominant hand has no part in the tablet writing stage, but the interaction between stylus and touch brings additional functionality to the writing experience in this project.

### Development Environment

The drawing app was developed on the Android system with Android Version Lollipop 5.1.1. We used the official Android IDE, Android Studio, and a private Github repository to manage version control. We wrote the code in Android Studio and ran it on our hardware device by installing Android Debug Bridge (ADB), allowing USB debug mode on our tablets, and connecting our tablets to our laptops by USB.

No 3rd party libraries were used. We used Android Graphics, a Canvas 2D component and other Graphics native components to build up our application.

### Tablet and Stylus

We borrowed the same tablet, Samsung Tab S2, from the Georgia Tech RNOC lab. The tablet has a 9.7” display and weighs 0.86lbs, which is suitable for note-taking. The styluses used were purchased through Amazon and are capacitive styluses compatible with many devices such as iPad and Samsung Tablets. The downside is that they are not active styluses that have special sensors built in to achieve more accurate detection or pressure sensitivity, but on the other hand, they do not need power and Bluetooth connection. An active stylus could not be used for this project since the tablet itself is not capable of detecting an active stylus and only responds to capacitive touch. Ideally, this project would have been done with an active stylus and a more sophisticated tablet such as an iPad so that touch sample tolerances would not have to have been used to distinguish the touch types.

### Thumb Tool Menu

A popular method of writing on a tablet is to have it propped on a stand so that the tablet is tilted towards the user and not entirely flat on the table. This means there is a natural feel to holding the tablet in the non-dominant hand while the dominant hand is writing. The tool described in this section is named the thumb tool menu due to the assumption that a user's hand would be resting on the tablet and the thumb would be the most accessible finger. However, this tool is not limited to the thumb, and in reality, there is no distinction between the thumb and any other finger. This means that if a user likes to write on a tablet entirely flat on the table, they can just hold any finger that feels natural to the screen to pull up the menu.

Upon the press and hold of any finger to the screen, a radial menu will appear centered on the finger’s placement. Once the menu appears, as long as the finger is held down, this menu will not disappear and will hold its location until the finger leaves the screen. The options on this menu are the following: Pen, Eraser, Marker (for highlighter), and Select.

Additionally, for Pen, Eraser, and Marker, as a user’s non-dominant finger is on the screen and displaying the radial menu, the tool's stroke width can be changed by dragging the stylus up and down on the screen (Figure 1). For example, if the user wants to have a red pen with a size of 10pt, then first the user will place their thumb on the screen. The user will drag their thumb to hover over “Pen” area, then drag over the red color section. As the user holds their thumb to the screen, they can take the stylus and drag vertically up or down anywhere on the canvas to change the tool's stroke width the same way a slider generally handles this. As the user slides their stylus up and down, the value of the tool width is shown numerically on the screen. Once the finger lets go of the canvas, the settings are sent to the CanvasUI object from the RadialMenu object. Selecting the Eraser is similar to Pen and Marker when changing its stroke width, but it does not have the additional arc-shaped menu for color. However, the Eraser does have a circle-shaped indication when the user draws an “Eraser stroke” on the screen(Figure 2), which Pen and Marker do not have.

![Figure 1](https://i.imgur.com/dCsq1Ef.jpg)
Figure 1: Pen and Marker tool with Radial Menu: Selecting the color by non-dominant hand and changing the stroke width by the stylus. The gray arrows indicate the stylus’s movement on the screen.

![Figure 2](https://i.imgur.com/UxplSI3.jpg)
Figure 2: The circle-shaped indication of the Eraser tool, and the strokes of Pen and Marker in the middle.

### Multi-touch Integration

The note-taking application looks out for multi-touch events from the non-dominant hand. While a single finger hold brings up the radial tool menu, two, three and four-finger taps are assigned different quick functions.

Inspired from Procreate, an advanced drawing application for the iOS, a two finger touch will trigger "undo". This allows a user to quickly undo something they just drew, saving time from having to select the eraser tool and dragging the stylus around manually for every small mistake. If done on accident, a three finger tap will trigger "redo". The undo/redo functionality is done by having the CanvasUI keep track of a “delete list” of Stroke objects. When undo is keyed, the most recent Stroke in the canvas stroke list is deleted and that Stroke is placed into the delete list. For redo, the most recently added Stroke to the delete list is added to the end of the Canvas Stroke list and removed from the delete list to be drawn again.

A four finger tap hides and shows the main static toolbar. Though the key to this application is the radial menu, a full toolbar should still be available so that quick colors and options can be set, and more advanced options can be selected. By allowing this toolbar to hide, this lets the user have the full screen be their canvas. A four finger tap is a fast way to bring the toolbar up, change some settings, and go back to primarily using the radial menu.

### Select Tool Expansion

This project accomplishes a basic select tool that performs this same functionality, but also accomplishes a new way to copy and paste (Figure 4). Once the select tool is chosen from the radial menu, a user can drag a dashed square around the object they want to move or copy. Once all desired objects are at least partially within the rectangle drawn, a user can tap within that rectangle and the rectangle will snap to fit over all selected objects as seen in Figure 3. Then the user can drag the object on the screen to move it to another location with their stylus.

The first rectangle drawn is just the initial selection rectangle. To determine what objects are within the selection rectangle, each Stroke object’s Android Path value is approximated into an array of points. Each point is iterated over and checked to see if it is inside the drawn rectangle. If any point of a Stroke’s Path is within this selection rectangle, then the entire Stroke object is considered selected. After drawing the initial selection rectangle, tapping the stylus within that rectangle creates a new dashed rectangle that fits around all objects selected. This is done by calculating all the bounding boxes of each selected stroke and calculating a new bounding box that uses the max and min points from this array of bounding boxes.(Figure 3)

![Figure 3](https://i.imgur.com/lTaegsk.png)
Figure 3: Create a selection, tap in bounds of the dashed rectangle and then move the selected strokes around.

The new copy function expands this basic selection functionality and works similarly to fanning cards out on a table. Once making a normal selection, copy and paste can be performed. The user can place the stylus onto the item being copied, and as they hold the stylus down, a finger can take and drag the object to the side. Copies of the drawing are stamped in increments and follow the path that the finger moves in. The longer and farther the item is dragged, the more copies are made. If the stylus drags out in a large "S" shape, then the copies will be stamped out in this "S" shape on the document, which is demonstrated in Figure 4.

![Figure 4](https://i.imgur.com/3AmH5Zy.jpg)
Figure 4: Multitouch copy and paste: the stylus holds onto the selected item and the non-dominant hand index finger drags along the gray line, making copies of the selected item along the trajectory.

Once copies are made and when the user lets go, all objects created will be left selected. This makes it easy for users to take their fingers or the stylus and rearrange each copy individually onto the canvas to their desired location. When the user is done rearranging, they can simply tap onto a not-active portion of the canvas (outside of any bounding box drawn) and deselect all the drawings.

### Conclusion

Overall, this application uses existing technology and APIs to conform a note-taking application to the user and their needs. Users are able to utilize the entire screen as their canvas, while being able to switch between popularly used tools naturally with the non-dominant hand that already rests near or on the tablet. Tool changes are faster, and balances the skill needed to operate the radial tool with minimal interruption time from the true task at hand: note-taking.