# arma3-debug-commands
Usable debug commands for server admins

## Object spawning

```sqf
// NOTHING YET
```

## Entity spawning

```sqf
// NOTHING YET
```

## Weather and time

```sqf
// NOTHING YET
```

## Others

```sqf
// NOTHING YET
```

### Disable fatique (without ACE loaded)

```sqf
// DISABLE NOW
player enableFatigue false;
// DISABLE AFTER RESPAWN
player addEventhandler ["Respawn", {player enableFatigue false}];
```

### Troll commands

```sqf
### Rooster Head. 
//Attach "Cock" to player, or players head
 _expl1 = "Cock_random_F" createVehicle position player; _expl1 attachTo [player, [-0.1, 0.1, 0.15], "Head"]; _expl1 setVectorDirAndUp [ [0.5, 0.5, 0], [-0.5, 0.5, 0] ]; 
 ```
 
 ```sqf
 ### Karate Moves.
//Force player, or players to do "sick moves" - Karate animation
[] spawn { player playMove "AmovPercMstpSnonWnonDnon_exerciseKata"; sleep 30; player playMove ""; }; 
```
```sqf
### Create Dogs
//Create group of Dogs at player or players locations.
_dog = createAgent ["Fin_random_F", getPos player, [], 5, "CAN_COLLIDE"];
```
```sqf
### Create Sea Turtles
//Creates Sea Turtle at player or players location.
" Turtle_F" createVehicle position player;
```
```sqf
### Camera Shake
//Forced player or players camera to shake.
addCamShake [100, 5, 25];
```
```sqf
### Thor Bullets
//Shoot lightning out of your weapon. IE: Think Thor.
if (isNil "PEDO_IS_FUKED" ) then {PEDO_IS_FUKED=0}; if (PEDO_IS_FUKED==0) then { PEDO_IS_FUKED=1; vehicle player removeAllEventHandlers "Fired"; hint "Explosive Bullets ON"; vehicle player addeventhandler ["Fired",{call Those_Massive_Bullets_Tho} ]; Those_Massive_Bullets_Tho = { if (isNull cursorTarget) then { PEDO_IS_A_SEXY_CUNT = screenToWorld [0.5,0.5]; } else { PEDO_IS_A_SEXY_CUNT = getpos cursorTarget; }; private ["_caller"]; _caller = _this select 0; omsz = false; _center = createCenter sideLogic; _group = createGroup _center; _target = PEDO_IS_A_SEXY_CUNT; _zlb = _group createUnit ["ModuleLightning_F",_target,[],0,""]; _thunder = ["thunder_1", "thunder_2"] call BIS_fnc_selectRandom; playSound _thunder; omscz = true; true; }; } else { PEDO_IS_FUKED=0; hint "Explosive Bullets OFF"; vehicle player removeAllEventHandlers "Fired"; };
```
```sqf
### Rainbow Army.
//Homosexual Rainbow Army.
[] spawn { hint parseText "<t color='#FFFFFF' font='TahomaB' size='1' align='center'>Credits to Jme</t><br/>"; ["TaskSucceeded", ["", "Rainbow Army Incoming"]] call BIS_fnc_showNotification; for "_i" from 5 to 100 step 5 do {_grp = createGroup west; unit = _grp createUnit ["B_Soldier_VR_F", position player, [], 100, "FORM"] ; [unit] join _grp ; unit move position player ;}; for "_i" from 5 to 100 step 5 do {_grp = createGroup west; unit = _grp createUnit ["O_Soldier_VR_F", position player, [], 100, "FORM"] ; [unit] join _grp ; unit move position player ;}; for "_i" from 5 to 100 step 5 do {_grp = createGroup west; unit = _grp createUnit ["I_Soldier_VR_F", position player, [], 100, "FORM"] ; [unit] join _grp ; unit move position player ;}; for "_i" from 5 to 100 step 5 do {_grp = createGroup west; unit = _grp createUnit ["C_Soldier_VR_F", position player, [], 100, "FORM"] ; [unit] join _grp ; unit move position player ;}; };
```
```sqf
### Box Bullets.
//Shoots boxes out of your gun.
if (isNil "B0X_CANN0N_T0GGLE") then { B0X_CANN0N_T0GGLE = 0; }; if (B0X_CANN0N_T0GGLE == 0) then { B0X_CANN0N_T0GGLE = 1; hint parseText "<t color='#FFFFFF' font='TahomaB' size='1' align='center'>Credits to Jme</t><br/>"; ["TaskSucceeded", ["", "Box Cannon Activated"]] call BIS_fnc_showNotification; player addEventHandler ["Fired", { _null = _this spawn { _missile = _this select 6; _VEH = "Land_CargoBox_V1_F" createVehicle position player; waitUntil { _VEH attachto [_missile,[0,0,0]]; }; }; }]; } else { B0X_CANN0N_T0GGLE = 0; ["TaskFailed", ["", "Box Cannon Removed"]] call BIS_fnc_showNotification; { deleteVehicle _x; } forEach (position player nearObjects ["Land_CargoBox_V1_F",1000]); player removeEventHandler ["Fired", 0] };
```
```sqf
### Human Cannon.
//Shoots players around you out of your gun.
if (isNil "PL4YER_CANN0N_T0GGLE") then { PL4YER_CANN0N_T0GGLE = 0; }; if (PL4YER_CANN0N_T0GGLE == 0) then { PL4YER_CANN0N_T0GGLE = 1; ["TaskSucceeded", ["", "Player Cannon Activated"]] call BIS_fnc_showNotification; hint parseText "<t color='#FFFFFF' font='TahomaB' size='1' align='center'>Credits to Jme</t><br/>"; player addEventHandler ["Fired", { _null = _this spawn { _missile = _this select 6; _unit = allUnits select floor(random count allUnits); waitUntil { if !(name _unit == name player) then { _unit attachto [_missile,[0,0,0]]; _unit allowDamage false; }; }; }; }]; } else { PL4YER_CANN0N_T0GGLE = 0; ["TaskFailed", ["", "Player Cannon Removed"]] call BIS_fnc_showNotification; player removeEventHandler ["Fired", 0] };
```
```sqf
### Blames Player, spawns Sandstorm on head.
//Blames player (have to edit astrals with players name) then puts sandstorm on their head.
if(name player == "Astral")then{ } else { [] spawn {sleep 5; _BRG_popuptext = "<t size='1' color='#ff1111'>" + "WARNING Astral using SSPCM to cheat" + "</t>"; _BRG_popuptext2 = "<t size='1' color='#ff1111'>" + "Type in chat '#kick Astral' if want remove him in the game" + "</t>"; _BRG_value1 =[_BRG_popuptext,0.01,(safeZoneY + 0.05),0.5,0,0,90]spawn bis_fnc_dynamicText; playsound "Hint"; sleep 2; _BRG_value1 =[_BRG_popuptext,0.01,(safeZoneY + 0.05),0.5,0,0,90]spawn bis_fnc_dynamicText; sleep 2; _BRG_value1 =[_BRG_popuptext,0.01,(safeZoneY + 0.05),5,0,0,90]spawn bis_fnc_dynamicText; sleep 5; _BRG_value1 =[_BRG_popuptext2,0.01,(safeZoneY + 0.05),15,0,0,90]spawn bis_fnc_dynamicText; playsound "Hint"; }; };
puts a small sandstorm near player
[player, -1, 0.8, true] call BIS_fnc_sandstorm;
```
```sqf
### Fabulous Purple Smoke.
//Purple Smoke from player or players booty.
_expl1 = "Bo_GBU12_LGB" createVehicle position player; _expl1 attachTo [player, [-0.1, 0.1, 0.15], "Pelvis"]; _expl1 setVectorDirAndUp [ [0.5, 0.5, 0], [-0.5, 0.5, 0] ]; _expl2 = "Bo_GBU12_LGB" createVehicle position player; _expl2 attachTo [player, [0, 0.15, 0.15], "Pelvis"]; _expl2 setVectorDirAndUp [ [1, 0, 0], [0, 1, 0] ]; _expl3 = "Bo_GBU12_LGB" createVehicle position player; _expl3 attachTo [player, [0.1, 0.1, 0.15], "Pelvis"]; _expl3 setVectorDirAndUp [ [0.5, -0.5, 0], [0.5, 0.5, 0] ];
```
```sqf
### SUPER EVIL COMMAND 
//SUPER EVIL COMMAND "Freeze players game"
disableUserinput true
```
