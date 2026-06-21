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

Go ahead and rename them to their uppercase versions, "Neck" and "Head".

<img width="635" height="434" alt="img41_rename_neckhead" src="https://github.com/user-attachments/assets/6931a61a-a7b8-43f3-923f-35fa649bae2e" />

I checked, and the Neck bends fine where it's at. We should move the head though, so move the Head bone so it lines up over Marth's joint.

<img width="1068" height="642" alt="img42_gif_movehead" src="https://github.com/user-attachments/assets/43d9e340-25b1-4917-b172-2a3e8f18bf50" />

At this point, Alf's model is scaled perfectly over Marth's skeleton! Or at least, perfect enough for Smash (close is close enough, remember?) 

And we've renamed as many of the bones as we could find that match!

<img width="1023" height="634" alt="img43_allscaled" src="https://github.com/user-attachments/assets/4e2dacae-cd8d-4a56-a428-2b4b7798a7ae" />

The thing about Blender poses is that they're not permanent changes right away. If you deleted the Alf armature, he'd snap right back into the position he was when we started.

To commit these changes to his Meshes, we need to Apply the Armature Modifier.

Before you continue, *you should save your Blender file as a new one to make a backup*, in case you mess up. I typically just add a new number at the end of the filename (2, 3, 4...)

Select the "AlfMain" Mesh in Object Mode to start, then find his Armature Modifier in the properties menu.

We still want him to HAVE an Armature Modifier when we commit the pose, so hover your mouse over his Armature Modifier and press Shift+D (or press the [V] dropdown -> Duplicate). This duplicates the modifier. Alf will suddenly lift his arms into the air if you did it right!

<img width="1046" height="848" alt="img44_dupe" src="https://github.com/user-attachments/assets/22ad5b2c-7f9a-4228-a255-fa2641bf64c1" />

Hover your mouse over the top modifier (or bottom, doesn't matter) and press Ctrl+A (or [V]->Apply) to Apply the modifier. 

<img width="1067" height="856" alt="img45_applytop" src="https://github.com/user-attachments/assets/a35ef4a6-2cb4-4034-8edc-e165c34295b3" />

Do this same process for all four of Alf's Meshes, until he looks like this:
Each should now have only one Armature Modifier.

<img width="1055" height="625" alt="img46_repeatapply" src="https://github.com/user-attachments/assets/6acff5d0-250b-44e7-ac99-783a3e07975d" />

This dupilicate+apply process permanently commits the changes you've made to the Mesh from the pose. If you deleted the armature now, Alf would stay in his T-pose. 

Do this dupe-apply process anytime you want to make permanent changes to the Mesh via Pose Mode.

Alf still has his arms raised because he's still "posed" in Pose Mode. To make his current pose the "unchanged" pose, select Alf's armature, enter Pose Mode, press A to select all bones, then Ctrl+A -> Apply Pose as Rest Pose. Alf will suddenly snap into a T-pose if you did it right.

<img width="935" height="571" alt="img47_applied" src="https://github.com/user-attachments/assets/4a173017-f421-479f-a100-340f474d6009" />

We're all done posing Alf and renaming his bones, so it's time to parent him to the Smash armature. Click the smush_blender_import orange stickman armature, shift+click all of Alf's Meshes, then Ctrl+P -> Object (Keep Transform) to parent.

<img width="1068" height="627" alt="img48_gif_parenting" src="https://github.com/user-attachments/assets/d577c979-1157-46f6-a051-e3198d8bb3e8" />

Next, we need his Armature Modifiers to pointed to the Smash armature. Go into the modifier for each Mesh and point Object to smush_blender_import.

<img width="711" height="756" alt="img49_repoint" src="https://github.com/user-attachments/assets/807cd47c-1028-488e-8035-8d0ce1728755" />

Since we've renamed Alf's bones to Marth's most of the Mesh should be waited. Alf did have some bones that *don't* have equivalents on the Smash armature, so they aren't weighted to anything yet. Alf's hair, for examples, has a bunch of bones that let the hair swing in Arc Rise Fantasia, but Marth's hair has completely different bones. They aren't in the same places, so we couldn't rename them to use them.

All that say, we need to see what on Alf's model is not weighted to Smash bones yet.

Like the last tutorial, enter Pose Mode and move the Hip bone back a ways. Everything that's weighted will move, anything that isn't will stay put.

<img width="834" height="751" alt="img50_movehip" src="https://github.com/user-attachments/assets/da2fcd03-cd97-44ea-9e42-a90f58a03057" />

Our job now is to weight all the vertices that haven't been weighted yet.
Let's start with Alf's head!

Select the AlfMain Mesh, enter Edit Mode, and turn on the Vertex selection mask (upper left icon, circled on the image. Also, turn on the Transparency viewport mode (upper right, circled icon).

Then, drag a box around all vertices that are sticking out from Alf's head:

<img width="1520" height="765" alt="img51_selectverts" src="https://github.com/user-attachments/assets/f7553cac-7d76-42ab-995a-bb33b10562ae" />

With the vertices selected, enter Weight Paint mode. Turn on the Vertex selection mask icon (upper left), which will turn all your selected Vertices white. Make sure the Weight setting is 1.0, too.

Open up the list of Vertex Groups for the Mesh to find and select Head.

<img width="1171" height="612" alt="img52_selectionmask" src="https://github.com/user-attachments/assets/c6bbda4d-9fbc-4431-abe3-0bc9daaffeec" />

Press Ctrl+x, then all those vertices will snap to his head. They're weighted!

<img width="742" height="622" alt="img53_weightedhead" src="https://github.com/user-attachments/assets/c832a778-66ef-439c-8e44-0f5c9b8f2601" />

We need to do the same exact thing, but with his arms now.

Select the vertices that are missing from his left arm, then weight all of them to ArmL. Do the same thing with Alf's right arm and ArmR.

<img width="748" height="665" alt="img54_getarm" src="https://github.com/user-attachments/assets/caa6f537-531c-4eca-a53f-e3e5f455e84c" />

<img width="821" height="604" alt="img55_weightedarm" src="https://github.com/user-attachments/assets/631e4b49-d767-4c3f-b091-2b09bf267a9a" />

And last, we have Alf's coattails. We COULD weight them simply to LegL, LegR, or Hip, but they'd look weird or stiff. 

<img width="821" height="474" alt="img56_noskirt" src="https://github.com/user-attachments/assets/c5fdfb6d-1b59-4a82-8851-8b15c5f5035d" />

You see, Smash Bros armatures sometimes have things called "Swing Bones". You know they're swing bones because they're blue, and all Swing bones must have names that begin with "S_". Swing bones, well, swing in-game, used for things like skirts, long hair, or tails. Unless you're adding new Swing Bones, you can basically treat Swing Bones as identical to normal bones.

Lucky for us, Marth has some Swing Bones that let the "skirt" of his tunic move. 

<img width="773" height="736" alt="img57_swingbones" src="https://github.com/user-attachments/assets/9258b864-8da0-4a47-a895-288023d2fe56" />

They're also in roughly the same place where Alf has his own "coat swing bones". We can re-use the weight from those Alf bones for Marth's Swing Bones.

<img width="707" height="606" alt="img58_alfswing" src="https://github.com/user-attachments/assets/a03ad176-5fd8-48de-a03d-7e812aabb46b" />

We really should have just renamed Alf's coat bones when we were doing the rest, but...
...well, you see, I forgot. :(

No matter! This lets me teach you even more techniques!

You can rename the Vertex Groups directly on the Mesh, and it's just like renaming the bones.
(We rename the bones first because that renames the Vertex Groups for ALL meshes automatically)

Scroll down the list of Vertex Groups for Alf and you'll see the weight and VGs for his coat bones are all still there.

<img width="1164" height="707" alt="img59_leftovers" src="https://github.com/user-attachments/assets/20f9e817-80d8-464a-947c-32fdebe9ccb6" />

To save time, I'll just tell you which Vertex Groups need to be renamed to what. 
On the left is the Alf Vertex Group, and on the right is what you rename it to.
Notice we're leaving two of them alone.


L_B_skirt_a -> S_ShirttailBL1
L_B_skirt_b -> S_ShirttailBL2
L_B_skirt_c (leave this alone for now)

L_F_skirt_a -> S_ShirttailFL1
L_F_skirt_b -> S_ShirttailFL2

R_B_skirt_a -> S_ShirttailBR1
R_B_skirt_b -> S_ShirttailBR2
R_B_skirt_c (leave this alone for now)

R_F_skirt_a -> S_ShirttailFR1
R_F_skirt_b -> S_ShirttailFR2

As you rename them, you should see parts of Alf's coat snap over to the rest of him. Again, it's because they are now weighted to Marth bones.

<img width="765" height="650" alt="img60_renamed_leftovers" src="https://github.com/user-attachments/assets/4e820d37-c16c-4714-b982-82706826bf6c" />

There's two little vertices on the ends of his coat that didn't get moved over. 

Select them in Edit Mode and weight them to S_ShirttailBR2 and S_ShirttailBL2 for their respective sides.

<img width="895" height="658" alt="img61_weightends2" src="https://github.com/user-attachments/assets/b83e2dce-9f92-4e8b-a0eb-824ad03c62c7" />

<img width="813" height="570" alt="img62_weightends3" src="https://github.com/user-attachments/assets/6fb6b709-73ad-4158-a62a-c371e67fb0ac" />

There's one more trick we're going to use.

The sides of Alf's coattails aren't weighted yet, but Marth doesn't have any Swing Bones on the sides. So, what we'll do instead is add the weight from Alf's side bones to the front Swing Bones.

We do this by adding another modifier (like Armature Modifier) called Vertex Weight Mix.
Add just in the modifiers by clicking [Add Modifier] -> Edit -> Vertex Weight Mix.

<img width="838" height="809" alt="img63_vertexmix" src="https://github.com/user-attachments/assets/9e2f49d4-52f0-44d0-96de-3335758a15ed" />

This modifer adds the weights from Vertex Group B to Vertex Group A. In the screenshot, you'll notice A is set to the Marth front-left swing bone (S_ShirttailFL1), and B is Alf's old side coat bone (L_S_skirt_a).

The other two things I've set are Vertex Set to All and Mix Mode to Add. When you set these, you'll see part of Alf's coat jump back over to Alf.

Hover anywhere in the box and press Ctrl+A to apply, or press [v] > Apply to commit the changes to the weighting.

When done, it should look like this:

<img width="774" height="855" alt="img64_applied" src="https://github.com/user-attachments/assets/29915076-fa0f-4568-935d-a695111a5bcc" />

Go ahead and do the same thing for S_ShirttailBL2 and L_S_skirt_b as below:

Repeat the process also for Alf's right side, ShirttailBL1/2, R_S_skirt_a/b.

<img width="805" height="628" alt="img65_nextmix" src="https://github.com/user-attachments/assets/310bcf96-6780-4fbb-8412-2183dd2babe4" />

When you're finished with both sides, you'll see just this one spot left unweighted on Alf:

<img width="913" height="724" alt="img66_allmixed" src="https://github.com/user-attachments/assets/4035856c-0e8f-4582-863c-035839bc5727" />

We could just weight those vertices to Hip. However, I'll use this chance to tell you about the Smash bone LegC. LegC is basically the same thing as Hip, but I think it's supposed to control the legs rather than the whole Mesh. I've never seen the two bones used differently. You can usually just ignore LegC, but in this case we can use it to our advantage.

In AlfMain's Vertex Groups, find the lowercase "hip" entry.

<img width="728" height="843" alt="img67_oldhip" src="https://github.com/user-attachments/assets/d92c1b8f-45f8-450d-b3cb-9fbd26fe8270" />

Rename that bone to "LegC", and it should weight most of it. There may be some vertices left unweighted, so just go ahead and weight them to LegC as well.

<img width="741" height="503" alt="img68_legc" src="https://github.com/user-attachments/assets/c78666b7-ad4c-4df0-ac78-a00637febbdb" />

<img width="714" height="460" alt="img69_weightagain" src="https://github.com/user-attachments/assets/b2fd1fd1-1e00-43da-b170-e73c11c6bcdd" />

And with that, we've weighted all of Alf's body! Hurray!

<img width="432" height="736" alt="img70_weightedbody" src="https://github.com/user-attachments/assets/b2cfc7ad-6074-4f1a-93fd-6bf51b5185ab" />

Now, for his sword, and more importantly, its name.

You see, by default, any Meshes that don't use vanilla Smash Mesh names (i.e. all the ones we've added so far), will always be present on the Mesh.

This means that, with the sword being named "AlfSword", it'll always be on his model at all times, even when he's clapping or holding something else. And we don't want that!

What we'll do is rename Alf's sword Mesh so that it has the exact same name as Marth's sword Mesh, which will make the game treat it just like Marth's sword.

For the sword in his hand, Marth actually has two Meshes, 

WeaponbladeM_VIS_O_OBJShape and WeapongripM_VIS_O_OBJShape

<img width="815" height="692" alt="img71_marssword" src="https://github.com/user-attachments/assets/e2a62781-3519-45fd-b4ad-648b759a35f9" />

Either name will do. And there's no need memorize the names or anything. I always copy and paste the name from the existing Smash Mesh. You can even copy the names from this tutorial and paste them in.

You can also notice that his sword is weighted to the Sword1 bone.

<img width="871" height="545" alt="img72" src="https://github.com/user-attachments/assets/56d0a8a4-c30c-4773-8efe-13e56eb27de8" />

So go ahead and rename Alf's sword Mesh to either of Marth's names, I chose WeapongripM_VIS_O_OBJShape. Here's a gif of how I do it:

<img width="1031" height="696" alt="img73" src="https://github.com/user-attachments/assets/03d25548-a55f-4273-9c16-c817809c61a5" />

And then weight Alf's sword to Sword1.

<img width="862" height="603" alt="img73_weightsword" src="https://github.com/user-attachments/assets/c3bcade7-12de-4bd8-97ed-2c7b8292d390" />

So Marth also as ANOTHER Mesh for the sword when it's at his side, including a scabbard. Alf came with his own sword and scabbard, so we can easily replace it.

<img width="830" height="748" alt="img74_scabbard" src="https://github.com/user-attachments/assets/1640c825-6f7c-45da-85ca-2b8dc74a4390" />

Move Alf's sword-and-scabbard Meshes so that they're in roughly the same place as Marth's. Perfection isn't important here, just close enough.

<img width="722" height="417" alt="img75_gif_movescab" src="https://github.com/user-attachments/assets/5e863c00-b957-4fa6-91cf-c6bcefcf28f5" />

Rename the "AlfSword2" Mesh to tsuka_VIS_O_OBJShape, and weight it to the Vertex Group "Hilt".

<img width="794" height="650" alt="img76_scabbard" src="https://github.com/user-attachments/assets/0052b667-e4b7-4529-8c29-e50db1c2c8ff" />

Now we're really done! Alf is all weighted! Be sure to reset the pose in Pose Mode if you haven't done so already.

<img width="1012" height="624" alt="img77_alldone" src="https://github.com/user-attachments/assets/f7be84b9-9e09-434f-97bf-940edec695bf" />

Go ahead and convert all the materials on his Meshes, just the same as you've done in the last tutorial. 

<img width="1292" height="842" alt="img78_convertmat" src="https://github.com/user-attachments/assets/0d09496b-6684-4360-90b8-35336ee63e4b" />

Then export the model.

When you do, you're going to run into an (easily resolved) error. It'll look something like this:

<img width="1207" height="791" alt="img79_error" src="https://github.com/user-attachments/assets/36fc8fd6-3969-4304-9250-edca0d0265f2" />

It's telling you that the AlfMain Mesh has "Vertex with more than 4 weights" or whatever. I don't really understand why this is a problem, but the fix is super easy.

Select the AlfMain Mesh and go into Weight Paint mode. Then, press Weights -> Limit Total. A little box should appear in the bottom left corner. Click anywhere in the viewport to close it.

<img width="935" height="729" alt="img80_limitweights" src="https://github.com/user-attachments/assets/a91c4054-7514-491e-86f0-665916a34f86" />

That's it! You fixed it! You should be able to safely export him now, and open the model folder in SSBH.

<img width="1406" height="674" alt="img81_exported" src="https://github.com/user-attachments/assets/bf0e5fc5-2e1a-4da0-bc30-9269afca6e02" />

Now you can tweak Alf's material settings. For simplicity's sake, we'll just have all the material use the same settings. What's "good" for material settings can vary between models.

Pick any material and configure it with the settings like you see here:

<img width="1121" height="1016" alt="img82_mat" src="https://github.com/user-attachments/assets/d752186d-2284-487f-8a67-9edf092a4e06" />

Now, at the top of the window, click Material -> Add Material to Presets. This lets you copy the material settings as a template, so you can easily duplicate the same settings to other materials. 

Then, click on another material in the list, and press Material -> Apply Preset. Another window will appear, press the User tab, and select the material preset you created, then Apply.

<img width="1417" height="452" alt="img83_addpreset" src="https://github.com/user-attachments/assets/b09a967d-93d7-4f48-84ea-69a5d4a1d7de" />


Go ahead and do that to all of Alf's materials, and he'll be looking good in a snap!

<img width="1006" height="874" alt="img84_better" src="https://github.com/user-attachments/assets/8bc0dbbd-a46f-4a7f-b7ec-3ccb8c833400" />

And lastly, don't forget the name and config!

Open the mod folder in Smash Ultimate Mod Helper, PRESS THE CREATE CONFIG BUTTON, and then Create PRCXML to set his name up.

<img width="990" height="699" alt="img85_config" src="https://github.com/user-attachments/assets/1ab6dac6-c191-459f-8144-94a94280cc2e" />

And with that, Alf is complete. You can try it out in the game and see how it looks!

_"Now, my revenge will begin."_

<img width="577" height="699" alt="img86" src="https://github.com/user-attachments/assets/d5ab2f49-9933-452b-abeb-5d1f845531b3" />

<img width="724" height="541" alt="img87" src="https://github.com/user-attachments/assets/2881c87a-6fd9-490d-a3e1-d4aa159bdb6e" />

<img width="1266" height="709" alt="img88" src="https://github.com/user-attachments/assets/d9e07f21-3c24-42aa-b094-d02d8f6165b9" />




