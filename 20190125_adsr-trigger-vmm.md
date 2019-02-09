# 20190125_adsr-trigger-vmm

The scope of this project is to duplicate the transformations and orientations between VMM and Houdini.  

Rather than rewriting all of the VMM GL transformations in to something more "sane".  The goal of this project is to simply try to duplicate what I did in VMM in Houdini however backwards I coded it. The thought is if I am proficient enought to port my wonky matrices to Houdini then I would be ready to move on to making new content.  

Another goal of this project is to work the other way around.  I ported two tracks from VMM and tried to match their transforms and orientations exactly.   Now i want to create 2 more HDA assets in Houdini space and move those to VMM.   I think this will be a much easier direction to work.   

## FILES / FOLDERS

- 20190125\_triggerVMM Project
	- right now this project is just a metronome and VMM setting.  There are only 2 tracks that use .obj sequences 33,34. 
- HOUDINI
	- 1-1.txt 
		- This is the .chan file output from VMM\_timeline
	- CURRENT
		- adsr-trigger-vmm.hiplc
	- OLD FILES
		- dsr-trigger-vmm.hiplc - first tests
		- dsr-trigger-vmm_02.hiplc - more tests with attribute wrangles. there is some good code in these files.
		
- RENDER
	- VMM
		- render of a VMM animation from VMM_timeline. 

--

### 2019-02-09

Finally I had success mirroring the duplication and orientation of the 3d elements in VMM.  [output\_obj\_sequence.hiplc](/Users/lg3/BW_MCP/BW_LIB/HOUDINI/20190206_axis_of_frustration/output_obj_sequence.hiplc) has code that correctly orients the copies.  Suprisingly it was a lot simplier than I thought.  I still need to create point and attach geometry to them (Houdini likes that).  But it is effectively working.  Next step is to move this technique to a new file and setup both 3d elements.   One issue I noticed is that the "mirror" command aren't matching exactly.   For now I will just leave it at that.

**File:** [adsr-trigger-vmm.hiplc](/Users/lg3/BW_MCP/BW_PROJECTS/BW_PUBLISH/20190125_adsr-trigger-vmm/HOUDINI/adsr-trigger-vmm.hiplc)

Problems/TODO

- Mirror doesn't match in the "track2\_slideboxasset".  I suspect this happens with the orient_rot transforms are in negative space. Or it could be the original orientation of the HDA replicated asset.  I'm not sure the best way to fix this.   
- I still need to figure out the scale to match VMM.  I have the units all wrong and I'm just matching by eye.
- the "track" nodes should be turned into a HDA that accepts the other HDA animation asset.  Move all the controls to the root HDA track asset so it's truely "plug and play"
- I need to test out the chan import from VMM. 




### 2019-02-03

Today's I am still working on translating the matrix tranformations over to Houdini. I have spend time learning about @orient and copy-to-points.  In /Users/lg3/BW_MCP/BW_LIB/HOUDINI/20190203_orient-copies/ I was able to transform the way VMM does by changing the translation order to Trans, Rot, Scale.  I think this might solve my problems and get parity with VMM.

**File:** [dsr-trigger-vmm.hiplc](/Users/lg3/BW_MCP/BW_PROJECTS/BW_PUBLISH/20190125_adsr-trigger-vmm/HOUDINI/dsr-trigger-vmm.hiplc)

Changelog

- created copy new node:track2\_slidebox\_new
- track2\_slidebox\_old - not working
- could\_this\_be\_it - uses Transform Axis
- point\_wrangle\_tests - wrangle tests

Problems

- when you Local X it slighly changes the orientation which can be compensated with "Yaw"
- do not set local_Y to exactly 0.  you need to set this to 0.01

**File:** [dsr-trigger-vmm_02.hiplc](/Users/lg3/BW_MCP/BW_PROJECTS/BW_PUBLISH/20190125_adsr-trigger-vmm/HOUDINI/dsr-trigger-vmm_02.hiplc)

Changelog

- think\_i\_got\_it - still not rotating exactly like VMM.  Seems like the roll is not spinning the object orient on the z axis.  Yet there is still some good stuff in this file.
- drawing\_board - little bit closer.  There is an object_rotate node which both has quarterian rotate and translate on the same node.  This could be useful elsewhere. 

	