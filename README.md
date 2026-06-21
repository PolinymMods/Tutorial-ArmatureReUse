# How to Rig a Smash Model Using an Existing Armature

**Requirements:**

Attempted or Read Previous Tutorial:
https://gamebanana.com/tuts/19799

ArcExplorer (Extract model files)
https://github.com/ScanMountGoat/ArcExplorer/releases/tag/v1.4.5.1

Blender (3d modelling)
(My version) https://download.blender.org/release/Blender4.3/
(Latest) https://www.blender.org/download/

Smash Ultimate Blender Plugin
https://github.com/ssbucarlos/smash-ultimate-blender

SSBH Editor
https://github.com/ScanMountGoat/ssbh_editor

Smash Ultimate Mod Helper
https://gamebanana.com/tools/11259

Blender Template File (the better one):
https://github.com/PolinymMods/Tutorial-ArmatureReUse/blob/main/Alf%20Blend%20Template.zip

Model Template File (just the .DAE model):
https://github.com/PolinymMods/Tutorial-ArmatureReUse/blob/main/Alf%20Template%20(DAE).zip

Hello!

This is another beginner's guide to rigging models for Smash. Specifically, this tutorial teaches you how to re-use weights from a model's existing armature to rig your Smash character faster. This tutorial is going to be kinda long, as I'm trying to show you every step of the process. You're basically getting my 18 monthes of practice and training in a single tutorial!

My last tutorial showed you how to rig a model with no armature. In that tutorial, I taught the basics of rigging, like what "weighting" is, what files to import, etc. To try and not make this tutorial too big, I won't go back over some of the things already covered in the last one. 

This tutorial expects that you know:
 - How to move the camera around in Blender
 - How to select vertices and create selection masks
 - What Armatures, Meshes, and Vertices are
 - How to extract, import and export model files
 - How to parent an armature, and add an Armature Modifier to meshes
 - How to add vertex groups and add weight to them with selection masks
 - How to bend bones in Pose Mode, and clear the pose
 - How to convert materials, the optimal settings, and using SSBH

If don't know the above, go check out my last tutorial! :)

Before we begin, I'd like to make one important note: This tutorial uses the techniques I've deduced to be best from having worked on over 100+ mods. If you don't like the way I do something or you find a better way, feel free to try your own thing. There's many ways you can rig a model. The best way to learn new tricks in Blender is to just try stuff and see what happens! That's how I learned!

With that out of the way, let's get to the guide!

Are you ready? It's moon magic time!

For this tutorial, our mod is going to put Alf from Arc Rise Fantasia over Mars.

Oh yeah... his name's actually Mars, but we'll just use the "Marth" name Smash uses so there's no confusion.

Go ahead and use ArcExplorer to export the c00 body model folder, just like in the last tutorial. Only, use "marth" as the name instead of "ness". You can export the voice and UI files for good practice, or ignore them for now as I've provided some in the finished mod I'll linked to this tutorial.

Like last time, copy those exported files to one folder called "Marth", then duplicate that folder and rename the new one to "Alf over Marth (c00)". Inside the new folder, delete the contents of the "fighter/model/body/c00" folder so that none of the vanilla files will be left taking up space.

You should have two folders now looking like this:

<img width="475" height="251" alt="img1_folders" src="https://github.com/user-attachments/assets/52661038-93df-4d70-9483-fab9fc1454b9" />

Now you can open the template blender file I provided in the requirements, called "alf_template.blend". When you do, you should see something like this:

<img width="1195" height="620" alt="img2_import" src="https://github.com/user-attachments/assets/66f26ea1-1d2c-44ef-a0a1-d6329d035bbf" />

If that doesn't work for some reason, you can use the alternate .DAE file I've also provided. Simply import that DAE file into Blender, then import the body model folder from your "Marth" vanilla folder. Delete all of Marth's Meshes (except the sword in his hand, the scabbard, and sword hilt: hide those, you'll want their names later)

The main advantage of the Blender template file is that I've already hidden the bones on Marth's armature that you won't need to worry about. If you use the alternate file, then don't worry! It just means you'll see those extra bones.

So what we have now is Marth's armature, which should empty (save for those hidden meshes, if imported the armature yourself), and Alf's armature, which has some meshes attached to it.

Here's the plan of how we're going to rig Alf to be over Marth without weighting all of Alf's Meshes ourself:

## We will pose Alf's armature so that his Meshes line up neatly over Marth's bones.

## Then, we will rename the bones on Alf's armature, which renames the Vertex Groups, so that the weight from Alf's Vertex Groups works for Marth's Vertex Groups/Bones.

You'll notice that Alf's model is almost the same size as Marth's model. I've already gone ahead and scaled him so he'll fit nicely. When you import your own model, you'll have to do this yourself. It's tricky to know what size the model should be to make this armature re-use easier, which is why I've taken care of it for you.

Something else you'll notice is that Alf's bones are actually really tiny. Zoom in on his armature and you'll see what I mean:

<img width="1108" height="599" alt="img3_tinybones" src="https://github.com/user-attachments/assets/c3d227eb-a507-4f1d-a2b9-78f00dd1d8b0" />

They're a bit hard to spot that way in the Blender viewport. Luckily, you can see all of Alf's bones by looking through the tree in the object list:

<img width="949" height="632" alt="img4_bonelist" src="https://github.com/user-attachments/assets/30ba5d2a-c995-441a-bbaa-e838d9c3532b" />

Clicking on an item in the list on the right will select the bone in the viewport on the left. We're going to be selecting these bones a lot throughout this tutorial, so feel free to select them via the viewport or the list, depending on what's easier for you.

If you want to know what any of Alf's bones are for, select his armature, enter Pose Mode, and try rotating the bones.

<img width="945" height="606" alt="img5_gif_bendybones" src="https://github.com/user-attachments/assets/068ff6cb-f959-4a8c-a481-60c34fa9ac52" />

Now, here's an image to give you an idea of all the Marth bones we're going to use for our Alf mod:

<img width="916" height="819" alt="img6_marsbones" src="https://github.com/user-attachments/assets/faa04ee3-e141-412b-aeb9-c3b7fae77bd3" />

You can see this names show up on the bones of any armature by entering the properties menu (bottom right), click the green stickman icon, then find the Viewport display tab. This tab lets you change how the bones appear in your viewport. Click the Names checkbox to turn on or off the names display. You can play around with this menu at any time if you want to make bones look a little nicer for you.

<img width="675" height="672" alt="img7_togglenames" src="https://github.com/user-attachments/assets/6d910271-3cf0-4a60-9f13-b194c70f409f" />

So the way our little plan is going to work... Meshes move when they're weighted to Vertex Groups/Bones, right? That means Alf's bones are weighted to Alf's Vertex Groups. The thing is, Alf's bones are really similar to Marth's, just with different names. If we rename the bones, that renames the Vertex Groups automatically. By renaming the Vertex Groups to Marth's, we keep the weight paint but for new bones! You'll see how this works in action in a bit.

Let's start with Alf's leg bones.

Zoom in on his left thigh, and you'll see both Marth's LegL bone and Alf's L_thigh bone:

<img width="1056" height="616" alt="img8_legl" src="https://github.com/user-attachments/assets/9bea6a41-255c-4f38-a181-45672703e8da" />

I know from experience that the weight paint on Marth's bone is already in a good spot to bend well, being so close to Marth's leg bone. 

Right click Alf's L_thigh bone (or, double-click the name in the object list), then type the name "LegL" to rename it.

<img width="1059" height="606" alt="img9_gif_rename" src="https://github.com/user-attachments/assets/fb6e55b6-4d7a-44a0-80d8-991e3b0e4747" />

Do the same thing to the R_thigh bone on Alf's other leg. Rename it to LegR

<img width="1053" height="605" alt="img9_legr" src="https://github.com/user-attachments/assets/a9f26086-f4e8-4849-a5ac-d15b5ef771d7" />

Now let's look at their knee bones. Marth's KneeL bone begins at the little black dot, the joint, circled in green below. Alf's L_leg bone is a bit below that. 

<img width="1044" height="603" alt="img10_compare_knee" src="https://github.com/user-attachments/assets/0d236b32-3099-4e56-a430-c16b10818313" />
