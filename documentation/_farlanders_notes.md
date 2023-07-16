# Farlander's Notes
This document is here to give insight into what I was thinking with this mod. I know it's not great, but hey I want to be able to write my thoughts down in case shit goes south.
This documentation more or less works as follows. It will be split into categories either detailing thoughts or conventions in terms of what needs to be said or just stated. I really have no idea how to run this so i'm going to bother it and come back later.

## Focus Tree Conventions
While creating the focus trees for the mod, they went through an obnoxious amount of reformats; something I seem to do alot. I can safely say spending some time working on Hearts of Minecraft somewhat humbled my very tight style of code. Now I intend to make sure it's at least readable by someone else and easily readable in VSC and natepad++ (with the C++ langauge overlay).

The focuses are written as follows...

### Defining Focus Trees Containers
- Focus Tree IDs will always start with the TAG, an _, a short term to describe the tree's purpose (e.g.: willow for willow's tree, start for the initial tree, etc...), followed by focus_tree.
	- It should be noted that I try to make sure every tree under a single nation is consolidated in a debug version of the tree to display all the branches at once when developing. As such there should always be a focus tree with a _debug suffix encompassing all the branches. It means a bit of extra work to get it all working, but hey it's very VERY good for development.
- The focuses are then assigned with factor of 0 because otherwise it will be treated as higher than default which causes unfortunate issues.
	- The factor is then adjusted with a modifier encompassing either a tag, original_tag, or some other identifier to assign the focus tree apporpriately. An add weight must be used to make sure the focus tree shows up. By the mod's convention the weights are as follows. 2 is for a tree that will show initially. 3 should be used in junction with an aditional condition for loadable trees. 4 through 6 are reserved for any further additions if nessesary, though use of tags and conditions would be ideal. 7 should be used to designate debug trees only. Unless EAW screws with this convention, the weights should NEVER exceed 7.
	- If a submod is activated with EDR I would HIGHLY recommend creating a seperate focus tree container and adding the country flag *EDR_submod_active* to any countries being modified. The existing trees are designed to reduce their weights by 1 when this flag is active in a target country meaning submodded nations will load. This of course means that you will need to copy and modify the code that defines any desired focus trees should you wish to enable them. In all this should reduce patching overhead.
- The desired starting focuses should be added as a shared_focus entry. Keep in mind this must only be called for focuses that have no prerequisite focuses. Everything else should load so long as it chains to the called shared focuses.
- If applicable the continuous focuses should be added at the end. If it's an initial tree that will be replaced by another tree later, I recommend ommiting this.
### Defining Focuses
- Every focus should be a shared_focus so that it seamlessly can be called at a later date in multiple trees. Modularity is the name of the game and it seems to have no visible effect on loading time, just convienvce. I could be wrong, but i'm no CS major so take it with a grain of salt.
- When creating the focus keep in mind that each element should be listed by how it's read and displayed. To that end it should go as follows.
	- *id*
	- *icon*
	- *relative_poisition* if not at the top of a branch.
	- The *x* and *y* coordinantes along with the focus *cost*.
	- Any *allow_branch*, *prerequisite*, *available*, *bypass*, and other conditions.
	- *search_filters* if applicable.
	- *ai_will_do* if any.
	- *select_reward* and *completion_reward*.
		- It should be noted that EVERY completion_reward container should contain a log entry based on the following example. This will allow the game to log focus completion along with other major events for debugging in the HOI4 logs folder under the *game.log* to better diagnose issues down the line. This **MUST** be completed at all costs.
		*log = "[GetDateText]: [Root.GetName]: Focus Focus_ID"*
- The naming convention of focus IDs is based on the TAG_, a prefix letter(s) that designate branch (e.g. S for story, I for industrial, L for land army, N for navy, A for airforce, etc...), followed by two digits designating vertical position in the tree, and if applicable (which is likely) an additional two numbers to designate horizontal position within a branch. I am open to reinterpretation of the latter part of this system as it's a bit difficult to pair with event IDs. For consitancy with localisation keys the ID should **always** be upper case. This is because other file systems (Mac and Linux) are quite specific about spelling. I reckon that carries to windows as well.
## History File Conventions
###Country History Files
These files are often done in what I assume is a good load order. This could be wrong. Ah well. Stuff it!
- First we declare a capital. Every nation needs one.
[Continue Here]
### Notes
- Cult of Laughter gets moved to Our Town.
	- Theres a 5th, Nurgle Windigo's Sister.
		- Powerful. Influencial. Where did she go?
		- Nurgle is the lead. Went North.
		- She and her most loyal follower went North.
		- The coffin being moved is Pinkie Pies Corpse.
		- Our Town supplies down south.
		- This means the Cult splits per say. The Chaos gods stay in Ponyville and do their own thing. The Cult goes north and grows in Stalliongrad.
- Battle of Blood Falls (Red Falls).
	- Stalliongrad's first forray trying to take advantage of a weak Crystal Empire and Equestria.
	- They failed their offensive out west.
	- After a few years, they sneakily annexed Equestrian Territory after they broke apart.
- The last battle of the Crystal war caused a literal void. Taking ponies into it.
	- The few survivors are mentally scarred. Disproportionataly Earthies and maybe a few Pegs.
	- The Sisters and Sombra are still fighting.
- Advisors for Trotsylvania
	- Normally
		- Prince of Terror - Darthy
		- Captain of Industry - 
		- Ideological Crusader - 
		- Compassionate Grandee - 
		- Popular Figurehead - Radigus
		- Old Guard - Radigus
		- Head of Intelligence
	- Via Gladiatorial
		- Special Ops
		- Hill
		- MP
	- What Advisors do royals want?
		- 