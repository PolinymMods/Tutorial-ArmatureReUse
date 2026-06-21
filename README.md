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

Let's go ahead and rename Alf's L_leg bone to KneeL.

<img width="1038" height="603" alt="img11_rename" src="https://github.com/user-attachments/assets/d9e9d1f6-2c01-4727-89aa-1b402c5074b0" />

Even with just two bones renamed, we can now see how Alf's model will bend with the Smash armature this way! Don't believe me? Watch!

Select the "AlfMain" mesh, go to the modifiers menu (little blue wrench, bottom right), and change the Object field to "smush_blender_import". I call this, "repointing", pointing Alf's Armature Modifier to Marth's Armature.

<img width="1043" height="609" alt="img12_repoint_armature" src="https://github.com/user-attachments/assets/333b656f-afea-4339-a5a7-82b14ad6a21c" />

Select Marth's armature, go into Pose Mode, then try bending Marth's LegL and KneeL bones. You'll see Alf's leg and knee bend! Cool!
The rest of the Mesh doesn't move because it doesn't have any weight for Marth's bones yet.

<img width="1059" height="606" alt="img13_gif_kneetest" src="https://github.com/user-attachments/assets/5a6a9b79-ebbf-4605-971b-a1a03ed84c95" />

Something you'll notice is that Alf's knee bends a little funny. 

<img width="914" height="596" alt="img14_weirdbend" src="https://github.com/user-attachments/assets/416aedb2-649c-4dc6-ad27-cce2362d2a3d" />

See how it's kinda angular near the kneecap? 
I mean, if it looks fine to you you can leave it, but I don't like it. This is the perfect time for me to teach you the "Bone-Stretching" techinque!

First, make sure you reset the pose, then repoint the Armature Modifier to Alf's armature again.

<img width="1042" height="525" alt="img15_setback" src="https://github.com/user-attachments/assets/d59e1b99-729e-4e68-acc6-249b57ab82e3" />

Also, go ahead and rename Alf's R_leg bone to KneeR while you're at it.

<img width="1031" height="582" alt="img16_kneer" src="https://github.com/user-attachments/assets/69f567af-fc13-42bc-a328-ed69d29fa90d" />

Now, select both Alf's LegL and LegR bones. Either select by dragging a box around them in the viewport, or Ctrl+clicking in the object list.

<img width="1033" height="621" alt="img17_select_legs" src="https://github.com/user-attachments/assets/1132a480-f956-47d8-93b1-511286fc1934" />

Here's the plan: We'll using Bone-Stretching by literally "stretching" Alf's leg bone so that the joint of his knee bone lines up with Marth's. See the below image:

<img width="1020" height="696" alt="img18_moveplan" src="https://github.com/user-attachments/assets/30d930a1-df7e-48ac-988d-3528ca8e64eb" />
With both upper leg bones selected, select the Scale tool, grab the BLUE axis that appears (ONLY the blue one), and drag that blue axis until Alf's joints are over Marth's:

<img width="707" height="552" alt="img19_gif_resize" src="https://github.com/user-attachments/assets/efe0bc6f-ad6f-4601-989f-4899eed0663c" />

That is Bone Stretching, whenever you move bones like that to change the shape of the model. We used the scale tool here, but you can often just use the Move tool to stretch the bones, which gives better results when it works. Scale is what we want for this particular instance.

You may notice now that Alf's feet no longer touch the "ground". If you were to compare it to Marth's, you'd see the difference:

<img width="840" height="666" alt="img19_noground" src="https://github.com/user-attachments/assets/1bdaf460-1f49-4af3-b94a-d60162fb1f69" />

Before we fix that, let's rename the next bone for Alf's feet: Change the bone below his KneeL to be FootL. Do the same for his right side too, FootR.

<img width="1221" height="710" alt="img20_footl" src="https://github.com/user-attachments/assets/1eebec25-b72a-48ae-a14e-b4635c2c0973" />

Now we'll use bone stretching again, this time scaling his knees, so that his feet will touch the ground again. You can use the green line on the Blender viewport grid as a reference for where the "floor" is.

<img width="1250" height="736" alt="img20_gif_touchgrass" src="https://github.com/user-attachments/assets/b57d5d3e-7cf7-467c-8223-961014d45a45" />

Finally, rename Alf's toe bones to be ToeL and ToeR. They're already lined up pretty well. Toe bones aren't super important, but they're often easy to rig.

<img width="1228" height="723" alt="img21_toel" src="https://github.com/user-attachments/assets/27b5fc33-ef18-4f78-8eb1-b07d9227a0ec" />

With both legs done, let's start moving further up on Alf.

<img width="891" height="662" alt="img22_alfhip" src="https://github.com/user-attachments/assets/64e6709d-3c82-4d9d-8470-a8c41e56e01b" />



