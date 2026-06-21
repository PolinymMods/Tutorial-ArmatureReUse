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

You may notice that Alf has a bone called "hip", in lowercase. 
We won't use this bone for his "Hip" bone on Marth for this tutorial, but you could. We'll actually rename the Vertex Group for it directly later to show you how that's done. All that to say, you can ignore it for now.

We're interested in Alf's "spine_a" bone. There's a lot of bones clustered in the hip area, so it'll be easier to find if you look in the list.

<img width="873" height="750" alt="img23_spinea" src="https://github.com/user-attachments/assets/8111c73c-13a7-4ce2-917b-422c94e618b8" />

We'll rename THAT bone to "Hip". That capital H is important, don't forget it!

<img width="703" height="736" alt="img24_hip" src="https://github.com/user-attachments/assets/57e1cfb4-d282-4d96-9622-6a9f80bea986" />

The next bone connected to that one, spine_b, is right around Marth's Waist. So, rename it to "Waist". 

<img width="1071" height="684" alt="img24_waist" src="https://github.com/user-attachments/assets/8fa0a2e3-a04a-4287-9e38-525c797450ff" />

spine_c should be renamed to "Bust".

<img width="1108" height="718" alt="img25_bust" src="https://github.com/user-attachments/assets/1b594f0b-8309-4993-925f-a407361ee064" />

The bone between Alf's chest and left arm equates to Marth's ClavicleL, so rename it.

<img width="1115" height="727" alt="img26_claviclel" src="https://github.com/user-attachments/assets/fab6dbee-ba53-4df1-9d11-f2e023c5e2ec" />

That leads us now to his shoulder joint, which should be "ShoulderL". 

<img width="1003" height="558" alt="img27_shoulderl" src="https://github.com/user-attachments/assets/0605ef64-3ee2-40b6-82c8-f639b0784ac9" />

You may have noticed by now that Alf's model is in an A-pose (his arms pointed down like the letter A), while Marth's is in a T-pose (arms straight out). 

But I do not like that. That's not good, Cecil. 

<img width="782" height="627" alt="img28_apose" src="https://github.com/user-attachments/assets/4a732198-5169-4059-a81e-849a2ca5a7ea" />

We can just pose Alf's armature to fix that!

First, in Pose Mode, grab Alf's shoulder bone and move it up to where Marth's ShoulderL begins.

<img width="947" height="736" alt="img29_0_gif_moveshoulder" src="https://github.com/user-attachments/assets/996b2a65-98dc-48eb-99aa-ee995e70cfed" />

Next, with the same bone selected, use the Rotate tool to bend it so it's straight out just like Marth's. Try to get it as close as you can, but don't sweat it too much. You can hold Ctrl while bending the bone to move it only in specific degree amounts for better control.

<img width="947" height="736" alt="img29_a_gif_movearm" src="https://github.com/user-attachments/assets/87ddc2ad-10a3-4ea6-b00f-526dc72ee824" />

Once his arm is straight out, look down Alf's arm to find the bone where his elbow is. That bone should be renamed "ArmL".

<img width="1152" height="597" alt="img30_arml" src="https://github.com/user-attachments/assets/011495da-6ac7-49f6-accb-374e48891341" />

We'll bone-stretch his ArmL so its joint lines up with Marth's. This time, you can use the Move tool instead of Scale. We want to avoid using scale here because it would also scale his hand and fingers, which we don't want.

<img width="832" height="736" alt="img31_gif_movearm" src="https://github.com/user-attachments/assets/9de31c8b-e814-4c4b-813f-c816ca3cb7b8" />

Look further down Alf's arm to find the bone where his wrist is. Name this one HandL.
It's already pretty close to Marth's HandL, so we don't need to move it.

<img width="1016" height="434" alt="img31_handl" src="https://github.com/user-attachments/assets/5614a408-31d9-4dd3-a1b5-ef36a61acac1" />

Now we have to talk about fingers. Fingers aren't fun. :(

I mean, they look nice when they work, but your custom model's fingers will be a different size than the Smash fingers nearly every single time. 

It won't exactly be pretty, but we can fix it. 

First up, here's the names for Smash fingers.

<img width="1231" height="698" alt="img32_fingers" src="https://github.com/user-attachments/assets/a1d695b5-8e5c-4af7-ae3b-7824f8269e45" />

Each Smash finger is comprised of three bones.
So, the index finger is made up of bones Finger11, Finger12, Finger13.
The pattern is the same for all other fingers, so the pinky finger for example is FingerL41, FingerL42, FingerL43.
The only difference for the right hand is that it's FingerR11, FingerR12, and FingerR13.

(The "zero" fingers, Finger L10, Finger R20, etc., don't matter. You can hide them on the skeleton and ignore them completely.)

Go ahead and rename all of Alf's fingers so that they match Smash's naming. Yes, even though they don't line up completely yet. We're about to fix that:

<img width="1331" height="718" alt="img33_fingers2" src="https://github.com/user-attachments/assets/89954afb-ee8b-4308-b27c-40c171174b37" />

When you're done, Alf's finger bones should look like this:

<img width="831" height="632" alt="img34_rename_bones" src="https://github.com/user-attachments/assets/56cf4643-7c17-4c07-8219-dfccd72d1927" />

Here's the unpleasant part: Now move all of Alf's finger bones so they line up with the equivalent Marth bones. The Gif below shows me doing it. Use the Rotate tool on the thumb bones. Just try your best to get them as close as you can, but again, don't worry it getting it perfect. You probably won't notice anything wrong in-game.

<img width="464" height="385" alt="img35_gif_movefingers" src="https://github.com/user-attachments/assets/ca138f20-dd23-4f87-8512-6a38ee33129f" />

Your Alf finger bones should end up kinda like this:

<img width="718" height="597" alt="img36_newfingers" src="https://github.com/user-attachments/assets/ac1fe54f-8fde-4cf2-a47a-fbc94c08eaf4" />

In regards to the vertical axis, Alf's bones are pretty close to where Marth's are (pretty close is close enough). 

<img width="662" height="423" alt="img37_yview" src="https://github.com/user-attachments/assets/ed99ed56-0315-41e8-ba69-b4cd68c434f6" />

We should move his thumb, though. Move and rotate the bones like you did from top-down so the joints line up.

<img width="686" height="563" alt="img38_rotate" src="https://github.com/user-attachments/assets/beccc44f-fb0f-4711-bf2b-a7699fbf33d1" />

With that, his left arm should be good to go.

To save space on this tutorial, I won't cover doing the right arm. Just do exactly what you did with the left arm, but use R in the place of all the bones with L in the name. You know the drill!

Again, don't worry about getting his arms perfectly symmetrical. You won't notice if it's wrong. Remember the Smash modding motto:

CLOSE IS CLOSE ENOUGH!

<img width="894" height="634" alt="img39_bothsides" src="https://github.com/user-attachments/assets/234dd20d-d9a2-4ad2-a40d-6eb020b84374" />

Now we can move on to Alf's neck and head.

Comparing the bones, they're pretty close already. In fact, Alf's bones are even named "neck" and "head" in lowercase!

<img width="1063" height="629" alt="img40_neckhead" src="https://github.com/user-attachments/assets/b904d91b-ecf2-4c0d-b84f-4040c3a3447a" />







