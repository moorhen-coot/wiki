---
layout: post
title: "Creating Figures with Moorhen"
date: Fri 3 Nov 16:08:00 GMT 2023
---

## Introduction

This tutorial will explain how to make high-quality figures of molecular models, maps, and analysis/validation markup with Moorhen.
Load tutorial data 1 into Moorhen by:

Begin by clicking on the Moorhen burger icon and then 
 clicking on the "File" button and selecting "Load tutorial data" and then selecting tutorial 1 and clicking "OK". You should see something like this:

![layout](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Initial-View.png)

This shows a cylinder representation of the model and a chickenwire representation of the electron density. 

Moorhen allows you to have finer control over what is drawn. For instance there are more representations available and we can turn them on or off from the "Models" and "Maps" dialogs.

We will begin by turning off the electron density map to allow us to see the model more clearly. To do this first click on "Maps" in the menu. You should see this:

![layout](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Map-Dialog.png)

Turn off the maps by clicking on each of the eye icons. The slashes in the eyes will disappear and the maps will be hidden:

![layout](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Maps-Hidden.png)

Click on the "X" in the top right of the "Maps" dialog to dismiss it.

### Switching representation style

Click on "Models" in the left-hand menu to show the "Models" dialog.

![layout](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Model-Dialog.png)

The "Bonds" button is highlighted to show that bonds are being drawn. CVlick on this to hide the bonds and then click on "Ribbons" to show ribbons.

![layout](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Ribbon.png)

Try the "C-As", "Gauss.", "Surf." and "Spheres" buttons.

## Colour Schemes

The model representations shown so far have been coloured with a default colouring scheme: colour by chain mode. Moorhen allows you to change the colour scheme.

Click on the "colour bucket" icon ![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Colour-Bucket-55.png) to the right of the atom representations buttons. This will display the colour edit dialog showing the current colour rules.

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Colour-Dialog.png)

The lower section shows the current colour rules. Each colour rule  supersedes the rules above it. To demonstrate this we will create a new colour rule. First change the "Rule type" from "By molecule" to "By atom selection". An "Atom selection" box appears, type "//A/87-298" into this box. Choose a new colour e.g. bright green from the colour picker to the right. Click "Add rule". The helical domain will turn bright green and your new colour rule appears at the bottom of the list of rules.

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Colour-Rules.png)

(Clicking on the up arrow of this rule to make it go up the list will mean that is will be superseded by Rule 2 and the model will change back to previous appearance.)

## Additional Representations

Sometimes you may wish to add additional representations, e.g. to display only a subset of the atoms in a particular style. To do this, click
on the "+" button to the right of the main representation buttons. A new dialog will appear.
![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Additional-Repr.png)

In the new dialog you can select "Style" and "Residue selection" for the new representation.
Change "Selection" to "Spheres" and "Residue selection" to "Residue Range". A "Chain" selector and sequence viewer will appear.

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Additional-Repr-Sequence.png)

The sequence viewer may be scrolled left and right by clicking on it and dragging. Move it around and then click on residue number 50 (R), then **shift-click** on residue number 65 (K). Two triangles connected by a line will appear - this represents the residue range selected.

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Additional-Repr-Sequence-Selected.png)

Then click on the "Create" button at the bottom of the dialog. The new spheres will be drawn and a button labelled "Spheres //A/50-65"
which allows you to hide/show the spheres (like the main representations) will be shown in the "Models" dialog.

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Additional-Repr-Spheres.png)

The new button also has "pen" and "dustbin" parts. The "pen" allows you to edit the atom selection/colouring/style;
the "dustbin" deletes the new representation. Click on the pen and then uncheck the "Apply general colours settings" button. You
will a new drop down menu, this will be set to "User defined colour":

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Additional-Repr-Custom-Colour.png)

Click on the green square to the right of this menu. A colour picker will appear. Pick a new colour (e.g. a shade of purple) 
and then click "Apply". Your spheres (and the representation hide/show button) will change colour.

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Additional-Repr-Custom-Colour-Applied.png)

Now hide the new spheres and the default bond representations by clicking the appropriate buttons in the "Models" dialog. Then create a
new "Ribbons" representation coloured by temperate factor. First click on "+" again and then use the following settings:

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Additional-Repr-Ribbon-BFactor-Settings.png)

Then click "Apply":

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Additional-Repr-Ribbon-BFactor.png)

## Ball and Stick Variants

There are many options to customize the drawing of both maps and models. We begin here by showing how to change some settings for
the drawing of "Bonds" model representations. Click on the gear wheel button ![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Model-Gear-Wheel.png) to the right of the atom representations buttons. A large dialog with many options will appear:

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Model-Options.png)

The top slider ("Bond width") controls the thickness of the bond. The second slider ("Radius-Bond ratio") changes the relative size of
the sphere drawn at each atom position to the bond. Try changing these two sliders to about 0.2 and 2.0 respectively. Your "bonds" will
change to balls and sticks.

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Ball-And-Stick.png)

The third slider in the settings dialog varies the smoothness of the cylinders drawing the bonds. The effect of this slider
will be most noticed in close up scenes. Zoom in closely and rotate the scene so that you can see a bond/sphere intersection
clearly:

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Ball-And-Stick-Close.png)

Now change "Bond Smoothness" to smooth to produce a much rounder cylinder:

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Ball-And-Stick-Close-Smooth.png)

## Symmetry

Molecular models obtained from crystallographic methods calculations normally contain information about the symmetry of the
crystal. This information can be used to display symmetry mates of the molecule. Zoom the view out so that there is space around 
the view of the molecule. Click on the gear wheel icon (described in previous section) to show the draw settings. 

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Before-Symmetry.png)

Then turn on the "Show symmetry mates" button. This will show symmetry mates within the distance specified by the "Symmetry Radius"
slider immediately below. Play around with the radius.

![](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Symmetry.png)

## Surfaces

While completing previous sections you may have noticed buttons labelled with "Surf." and "Gauss." among the different representation styles for a molecule. These buttons let you display your model as a surface. Let's first try to draw a Gaussian surface. Go to the "Models" window and click on the button labelled with "Gauss.".

_Moorhen displays the model as a Gaussian surface._

![gauss. surf. screenshot](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Gauss-Surf.png)
Note: Notice how we have turned off Bond representations to have a better view of the surface. We have also changed the "Scene preset" to figure making.

Moorhen lets you modify the different parameters used to calculate this surface (and therefore the way it looks) under the settings menu. To open this menu, click on the wheel button in the "Models" window. You can find this button right under the colour schemes button and on top of the additional represetations button.

_Moorhen displays a popover with different representation settings._

![gauss. surf. settings screenshot](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Gauss-Surf-Settings.png)

Right under the settings for the bond representations and above the settings for model symmetry, we find a series of sliders for different parameters labelled "Gauss. Surf." Try to move the different sliders and see how the Gaussian surfaces changes. By applying these changes Moorhen gives us full control of how the surface is contoured.

Let's now try a different type of molecule surface representation. Turn off the Gaussian surface by clicking on the "Gauss." button and turn on the "Surf." representation button. Don't worry if this takes a bit of time, the calculations involved in this representation are more complex than Gauss. surfaces.

_After a few seconds, Moorhen displays the model as a molecular surface._

![surf. screenshot](https://raw.githubusercontent.com/moorhen-coot/blog/main/images/Moorhen-Figure-Tutorial-Surf.png)

Moorhen has now combined the van der Waals surfaces of the atoms in the molecule into a single surface representation. As you can see, this representation offers great detail of the surface area of the biomolecule that is accessible to solvent, or in other words the so-called solvent-accessible surface area (SASA). Can you spot any big solvent-exposed cavity in the molecule's surface where a ligand could potentially bind?

## Maps and map masking

Style, colour, transparency, contour level, radius, 

## Validation and Analysis

## Clip, Fog and Lighting Effects

## Preferences

## Saving your image

## Video Recording
