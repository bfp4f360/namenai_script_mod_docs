
# <span style="color:gold">Welcome to Namenai Script mod Mkdocs site</span> 	
Hello this is a simple mkdocs site for the NSM (Namenai Script Mod).

Also this is the link to the fancy mkdocs site [here](https://namenai-script-mod-docs.readthedocs.io/en/latest/)	
	
## <span style="color:gold">Mod links </span> 	
- This [here](https://steamcommunity.com/sharedfiles/filedetails/?id=2068356312) is the live mod.	

## Features

As of now theres only one feature, the jumppack. I plan to add other scripts like "energy shields" on uniforms/vest and vehicles and a generic afterburner script for jets/helicopters/vehicles. However these take time so big sad.


### Jumppack
There are 2 jumppacks. The XD-1 and XD-1 LTU. The difference is that the XD-1 LTU stands for "Limited Time Use" meaning you can only jump a select few times. This is because it has no energy regen. The onyl way to get energy back is to enter arsenal, ACE or BIS. If you do things like backpack on chest you will lose all energy, basicly anything where it spawns a new backpack. You can drop the backpack on the floor and it will retain its energy.

You can use CBA keybinds, just go to `Options > Controls > Configure Addons > NSM Jumppack Mod`. Of the 3, you only need to bind `jump` and one of `cycle left` or `cycle right`. The cycle buttons are like a weapon wheel in older games.

The way the jumppack works is, you select a jumptype (with `cycle left` or `cycle right`), and press `jump`. Thats fucking hard ye? You can even configure a jumptype to be directional, as in it jumps u in the direction you are looking. So if you look stright up it will jump you stright up, if you look down you will jump down. Non directional jumps follow a path independent of where you are looking, just in the direction you are facing.

You can do the following to have our own jumppack.

!!! info "Inheritance for own jumppack"	
    #### Example config.cpp	
    ```cpp	
    class CfgPatches	
    {	
        class my_cool_jumppack_patch	
        {	
            author="UR NAME HERE";	
            requiredAddons[]=	
            {	
                "NSM_patch_end"
            };	
            requiredVersion=0.1;	
            units[]={	
            };	
            weapons[]={};	
            vehicles[]={	
                "UR_COOL_NEW_JUMPPACK"	
            };	
        };	
    };	
    class CfgVehicles	
    {	
        class NSM_neutral_XD_1_backpack;	
        class UR_COOL_NEW_JUMPPACK: NSM_neutral_XD_1_backpack
        {
            scope = 2;

            // wowe daz me 😊
            author = "NSM";
            displayname = "[Jumppack] XD-1"; //Name this to whatever you want
            NSM_jumppack_is_jumppack = 1; // 1 means yes, 0 means no.

            // In seconds, I would not reccomend making 
            // this less then 1 just to account for user lag/network lag.
            NSM_jumppack_spam_delay = 1;

            // How much energy the pack has, think of like fuel.
            NSM_jumppack_energy_capacity = 200; 
            NSM_jumppack_recharge = 5; // How much energy per second is regenerated.

            
            // This is a little bit ugly
            // I wish there was a JSON/Dictonary
            // config way do doing this, but the 
            // cloest is hashmaps from CBA
            // but thats a script thing not
            // config, RIP cpp :)
            NSM_jumppack_jump_types[] = {
                {
                    "Forward Jump",// Name of jump
                    {
                        12,		//forward velo(0)
                        20,		//verticle velo(1)
                        50,		//cost(2)
                        0,		//angle(3)
                        0,		//directional(4)(no=0,yes=1)?
                        0		//can prone jump(5)(no=0,yes=1)?
                    }
                },
                {"Short Jump",{25,7,20,0,1,1}}
            };

            // I wouldnt reccomend changing these below.
            // Mainly because...idk. I just think its a little
            // bit complicated the way I set it up.
            // I will try to make it easier in future
            // to add stuff, mainly particle effects
            NSM_jumppack_jump_effect_script = "NSM_jumppack_effect_fnc_jt_21";
            NSM_jumppack_effect_points[] = {{"spine3",{0,-0.3,-0.1}}}; 
            NSM_jumppack_sound_ignite[] = {"NSM_Main\sounds\cdv21Start.ogg"};
            NSM_jumppack_sound_land[] = {"NSM_Main\sounds\cdv21End.ogg"};
            NSM_jumppack_sound_idle[] = {"NSM_Main\sounds\cdv21Idle.ogg"};

            //Obviously do watever u want here
            model = "NSM_Objects\Data\XD_1_Jumppack.p3d";
            maximumload = 100;
            hiddenSelections[] = {"camo1"};
            hiddenSelectionsTextures[] = {"NSM_Objects\Data\XD_1_JumpPack_CO.paa"};
            picture = "\NSM_Objects\icon.paa";
        };
    };	
    ```
    Or if your a lazy doo doo farted head, [here](/example.cpp) 💩


## Future

As I mentioned I plan to

1. Add a generic afterburner for jets/helis/vehicles
2. Energy shield for vehicles and players. Like Halo or some other bullshit sci fi shit 💩.