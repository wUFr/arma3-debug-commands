# arma3-debug-commands
Usable debug commands for server admins

## Object spawning

### Delete Object.
```sqf
//Will delete any object, or Vechicle your crosshair is at.
deleteVehicle cursorTarget
```

## Entity spawning

```sqf
// NOTHING YET
```

## Weather and time

### Skip Time
```sqf
// Skip time per hour. "5" = Hours (Server side)
skipTime 5; 
```
### Remove Fog
```sqf
//This will remove the fog from Arma completely, visually nice but will effect performance.
0 setFog 0; forceWeatherChange; 999999 setFog 0;
```

## Others

### Map teleport
```sqf
//This will teleport you around the map freely by alt then left clicking.
player onMapSingleClick "if (_alt) then {player setPosATL _pos}";
```
### God Mode
```sqf
//You will take damage, however you will not die. 
player allowdamage false;
```
### Upgrade Vechicles Speed
```sqf
// Will upgrade the speed of the current or active vechicles. Recommend god mode is on for this.
hint "Speed upgrade loaded!"; waituntil {!isnull (finddisplay 46)}; (findDisplay 46) displayAddEventHandler ["KeyDown","_this select 1 call MY_KEYDOWN_FNC;false;"]; MY_KEYDOWN_FNC = { _vcl = vehicle player; if(_vcl == player)exitwith{}; _nos = _vcl getvariable "nitro"; _supgrade = _vcl getvariable "supgrade"; if(isEngineOn _vcl) then { switch (_this) do { case 17: { if(isEngineOn _vcl and !isnil "_supgrade") then { _vcl SetVelocity [(velocity _vcl select 0) * 1.011, (velocity _vcl select 1) *1.011, (velocity _vcl select 2) * 0.99]; } else { _vcl setvariable ["supgrade", 1, true]; }; }; case 42: { if(isEngineOn _vcl and !isnil "_nos") then { _vcl setVelocity [(velocity _vcl select 0) * 1.01, (velocity _vcl select 1) * 1.01, (velocity _vcl select 2) * 0.99]; } else { _vcl setvariable ["nitro", 1, true]; }; }; }; }; };
```
### Kills Player.
```sqf
// Kills player, or player(s)
player setdamage 1
```
### Heal Player, or Player(s)
```sqf
//Heals yourself, or all players.
player setDamage 0;
```
### Removes all Weapons
```sqf
// Removes player, or player(s) Weapons.
removeAllWeapons player;
```
### Destory Targets
```sqf
//Will Destory whatever object at crosshair.
cursortarget setdamage 1
```

### Disable fatique (without ACE loaded)

```sqf
// DISABLE NOW
player enableFatigue false;
// DISABLE AFTER RESPAWN
player addEventhandler ["Respawn", {player enableFatigue false}];
```
### Repair Vechicle
```sqf
//Will repair any Vechicle you're currently in.
_timeForRepair = 0; _vehicle = vehicle player; hint format ["Please wait %1 seconds for repair/flip",_timeForRepair]; sleep _timeForRepair; if (_vehicle == player) then {_vehicle = cursorTarget;}; _vehicle setfuel 1; _vehicle setdamage 0; _vehicle = nil; vehicle = this select 0; _vehicle setvectorup [0,0,1];
```
### Remove Fuel from player, or player(s) vehicles.
```sqf
//This will remove all fuel from all active vechicles, or your own.
vehicle player setfuel 0;
```
### Add weapon to player or player(s)
```sqf
//This will add weapon via ID to player, or players.
player addweaponglobal "arifle_MX_GL_F";
```
### Set Player Ammo
```sqf
//This set current player, or player(s) ammo by adjusting the number.
player setAmmo [currentWeapon player, 1];
```
### See all people on the map
```sqf
//Will display ALL players and spawned units on the map.
if(stealthMarkerToggle == 1) exitWith {stealthMarkerToggle = 0; onEachFrame {}; {deleteMarkerLocal _x;} forEach markerList; hint "Markers disabled";}; stealthMarkerToggle = 1; markerList = []; markerUnits = []; hint "Markers enabled - Check map!"; while {true} do { if(stealthMarkerToggle == 0) exitWith {}; { _unit = _x; markerUnits = markerUnits + [_x]; _markerName = str(format ["%1",name _x]); _mName = "m" + _markerName; //player sidechat format ["%1",_markerName]; if(side _x == side player) then { _mName = createMarkerLocal [_markerName, position _x]; _mName setMarkerSizeLocal [0.6, 0.9]; _mName setMarkerShapeLocal "ICON"; _mName setMarkerTypeLocal "mil_triangle"; _mName setMarkerColorLocal "ColorBlue"; _mName setMarkerTextLocal _markerName; _mName setMarkerDirLocal (direction _x); markerList = markerList + [_mName]; } else { _unit = _x; markerUnits = markerUnits + [_x]; _mName setMarkerSizeLocal [0.6, 0.9]; _mName = createMarkerLocal [_markerName, position _x]; _mName setMarkerShapeLocal "ICON"; _mName setMarkerTypeLocal "mil_triangle"; _mName setMarkerColorLocal "ColorRed"; _mName setMarkerTextLocal _markerName; _mName setMarkerDirLocal (direction _x); markerList = markerList + [_mName]; }; //hint format ["%1",_mName]; } forEach allUnits; sleep 1; if(stealthMarkerToggle == 0) exitWith {}; {_x setMarkerPosLocal getPos (markerUnits select (markerList find _mName)); _x setMarkerDirLocal getDir(markerUnits select (markerList find _mName));} forEach markerList; sleep 1; if(stealthMarkerToggle == 0) exitWith {}; {_x setMarkerPosLocal getPos (markerUnits select (markerList find _mName)); _x setMarkerDirLocal getDir(markerUnits select (markerList find _mName));} forEach markerList; sleep 1; if(stealthMarkerToggle == 0) exitWith {}; {_x setMarkerPosLocal getPos (markerUnits select (markerList find _mName)); _x setMarkerDirLocal getDir(markerUnits select (markerList find _mName));} forEach markerList; sleep 1; if(stealthMarkerToggle == 0) exitWith {}; {_x setMarkerPosLocal getPos (markerUnits select (markerList find _mName)); _x setMarkerDirLocal getDir(markerUnits select (markerList find _mName));} forEach markerList; sleep 1; if(stealthMarkerToggle == 0) exitWith {}; {deleteMarkerLocal _x;} forEach markerList; markerUnits = []; markerList = []; };
```
### ESP
```sqf
//This will visually show lines to where all players and units are while on foot.
if (isnil ("WookieESP")) then {WookieESP = 0;}; if (WookieESP==0) then {WookieESP=1;cutText [format["Esp On"], "PLAIN DOWN"];hint "Esp On";}else{WookieESP=0;cutText [format["Esp Off"], "PLAIN DOWN"];hint "Esp Off";}; if (WookieESP==1) then { oneachframe { _nigs = nearestobjects [player,["CAManBase"],1400]; { if((side _x != side player) && (getPlayerUID _x != "") && ((player distance _x) < 1400)) then { drawIcon3D ["", [1,0,0,0.7], GetPosATL _x, 0.1, 0.1, 45, (format ["%2 : %1m",round(player distance _x), name _x]), 1, 0.03, "default"] } else { if((getPlayerUID _x != "") && ((player distance _x) < 1000)) then { drawIcon3D ["", [0,1,0.5,0.4], GetPosATL _x, 0.1, 0.1, 45, (format ["%2 : %1m",round(player distance _x), name _x]), 1, 0.03, "default"] }; }; } foreach playableUnits; _noobs = nearestobjects [player,["CAManBase"],100]; { if(((alive _x)) && ((player distance _x) < 100)) then { if((side _x != side player) && ((player distance _x) < 100)) then { if(player distance _x < 10 && _x iskindof "CAManBase" && side _x != civilian) then { drawLine3D [[getposatl player select 0, getposatl player select 1, getposatl player select 2], _x, [1,0,0,(abs((((player distance _x)) - 100)/100))]] }; } else { drawLine3D [[getposatl player select 0, getposatl player select 1, getposatl player select 2], _x, [0,1,0,(abs((((player distance _x)) - 100)/100))]] }; }; } foreach playableUnits; }; } else { oneachframe {nil}; };
```
### Show all Vehicles on the map with markers.
```sqf
//This will show ALL spawned Vechicles on the map. (Need testing if it updates in real time)
if (isnil "ggggggggggggggggggg" ) then {ggggggggggggggggggg=0};

if (ggggggggggggggggggg==0) then
{
hint "Adding Vehicle Markers";
ggggggggggggggggggg=1;
VL = vehicles;
j = count VL;
i = 0;
MV = true;

while {MV} do
{
VL = vehicles;
j = count VL;
i = 0;

for "i" from 0 to j do
{
veh = VL select i;
deleteMarkerLocal ("VM"+ (str i));
mk2 = "VM" + (str i);
mk2 = createMarkerLocal [mk2,getPos veh];
mk2 setMarkerTypeLocal "waypoint";
mk2 setMarkerPosLocal (getPos veh);
mk2 setMarkerColorLocal("ColorGreen");
mk2 setMarkerTextLocal format ["%1",typeOf veh];
};
sleep 0.5;
};
}
else
{
hint "VM Stopping";
i = 0;
MV = false;
ggggggggggggggggggg=0;

for "i" from 0 to j do
{
veh = VL select i;
deleteMarkerLocal ("VM"+ (str i));
};
```

## Troll commands

### Teleport player, or player(s) into the air.
```sqf
//Will teleport player, or all active players into the air based on set number.
_pos = getPosATL player; _pos set [2, 700]; player setPosATL _pos; player spawn bis_fnc_halo;
```

### Rooster Head.
```sqf
//Attach "Cock" to player, or players head
 _expl1 = "Cock_random_F" createVehicle position player; _expl1 attachTo [player, [-0.1, 0.1, 0.15], "Head"]; _expl1 setVectorDirAndUp [ [0.5, 0.5, 0], [-0.5, 0.5, 0] ]; 
 ```
### Karate Moves. 
 ```sqf 
//Force player, or players to do "sick moves" - Karate animation
[] spawn { player playMove "AmovPercMstpSnonWnonDnon_exerciseKata"; sleep 30; player playMove ""; }; 
```
### Create Dogs.
```sqf
//Create group of Dogs at player or players locations.
_dog = createAgent ["Fin_random_F", getPos player, [], 5, "CAN_COLLIDE"];
```
### Create Sea Turtles.
```sqf
//Creates Sea Turtle at player or players location.
" Turtle_F" createVehicle position player;
```
### Attaches GBU to Players.
```sqf
//This will attach bombs to player, or players. (Not tested if they explode)
_expl1 = "Bo_GBU12_LGB" createVehicle position player; _expl1 attachTo [player, [-0.1, 0.1, 0.15], "Pelvis"]; _expl1 setVectorDirAndUp [ [0.5, 0.5, 0], [-0.5, 0.5, 0] ]; _expl2 = "Bo_GBU12_LGB" createVehicle position player; _expl2 attachTo [player, [0, 0.15, 0.15], "Pelvis"]; _expl2 setVectorDirAndUp [ [1, 0, 0], [0, 1, 0] ]; _expl3 = "Bo_GBU12_LGB" createVehicle position player; _expl3 attachTo [player, [0.1, 0.1, 0.15], "Pelvis"]; _expl3 setVectorDirAndUp [ [0.5, -0.5, 0], [0.5, 0.5, 0] ];
```
### Camera Shake.
```sqf
//Forced player or players camera to shake.
addCamShake [100, 5, 25];
```
### Thor Bullets
```sqf
//Shoot lightning out of your weapon. IE: Think Thor.
if (isNil "PEDO_IS_FUKED" ) then {PEDO_IS_FUKED=0}; if (PEDO_IS_FUKED==0) then { PEDO_IS_FUKED=1; vehicle player removeAllEventHandlers "Fired"; hint "Explosive Bullets ON"; vehicle player addeventhandler ["Fired",{call Those_Massive_Bullets_Tho} ]; Those_Massive_Bullets_Tho = { if (isNull cursorTarget) then { PEDO_IS_A_SEXY_CUNT = screenToWorld [0.5,0.5]; } else { PEDO_IS_A_SEXY_CUNT = getpos cursorTarget; }; private ["_caller"]; _caller = _this select 0; omsz = false; _center = createCenter sideLogic; _group = createGroup _center; _target = PEDO_IS_A_SEXY_CUNT; _zlb = _group createUnit ["ModuleLightning_F",_target,[],0,""]; _thunder = ["thunder_1", "thunder_2"] call BIS_fnc_selectRandom; playSound _thunder; omscz = true; true; }; } else { PEDO_IS_FUKED=0; hint "Explosive Bullets OFF"; vehicle player removeAllEventHandlers "Fired"; };
```
### Rainbow Army.
```sqf
//Homosexual Rainbow Army.
[] spawn { hint parseText "<t color='#FFFFFF' font='TahomaB' size='1' align='center'>Credits to Jme</t><br/>"; ["TaskSucceeded", ["", "Rainbow Army Incoming"]] call BIS_fnc_showNotification; for "_i" from 5 to 100 step 5 do {_grp = createGroup west; unit = _grp createUnit ["B_Soldier_VR_F", position player, [], 100, "FORM"] ; [unit] join _grp ; unit move position player ;}; for "_i" from 5 to 100 step 5 do {_grp = createGroup west; unit = _grp createUnit ["O_Soldier_VR_F", position player, [], 100, "FORM"] ; [unit] join _grp ; unit move position player ;}; for "_i" from 5 to 100 step 5 do {_grp = createGroup west; unit = _grp createUnit ["I_Soldier_VR_F", position player, [], 100, "FORM"] ; [unit] join _grp ; unit move position player ;}; for "_i" from 5 to 100 step 5 do {_grp = createGroup west; unit = _grp createUnit ["C_Soldier_VR_F", position player, [], 100, "FORM"] ; [unit] join _grp ; unit move position player ;}; };
```
### Box Bullets.
```sqf
//Shoots boxes out of your gun.
if (isNil "B0X_CANN0N_T0GGLE") then { B0X_CANN0N_T0GGLE = 0; }; if (B0X_CANN0N_T0GGLE == 0) then { B0X_CANN0N_T0GGLE = 1; hint parseText "<t color='#FFFFFF' font='TahomaB' size='1' align='center'>Credits to Jme</t><br/>"; ["TaskSucceeded", ["", "Box Cannon Activated"]] call BIS_fnc_showNotification; player addEventHandler ["Fired", { _null = _this spawn { _missile = _this select 6; _VEH = "Land_CargoBox_V1_F" createVehicle position player; waitUntil { _VEH attachto [_missile,[0,0,0]]; }; }; }]; } else { B0X_CANN0N_T0GGLE = 0; ["TaskFailed", ["", "Box Cannon Removed"]] call BIS_fnc_showNotification; { deleteVehicle _x; } forEach (position player nearObjects ["Land_CargoBox_V1_F",1000]); player removeEventHandler ["Fired", 0] };
```
### Human Cannon.
```sqf
//Shoots players around you out of your gun.
if (isNil "PL4YER_CANN0N_T0GGLE") then { PL4YER_CANN0N_T0GGLE = 0; }; if (PL4YER_CANN0N_T0GGLE == 0) then { PL4YER_CANN0N_T0GGLE = 1; ["TaskSucceeded", ["", "Player Cannon Activated"]] call BIS_fnc_showNotification; hint parseText "<t color='#FFFFFF' font='TahomaB' size='1' align='center'>Credits to Jme</t><br/>"; player addEventHandler ["Fired", { _null = _this spawn { _missile = _this select 6; _unit = allUnits select floor(random count allUnits); waitUntil { if !(name _unit == name player) then { _unit attachto [_missile,[0,0,0]]; _unit allowDamage false; }; }; }; }]; } else { PL4YER_CANN0N_T0GGLE = 0; ["TaskFailed", ["", "Player Cannon Removed"]] call BIS_fnc_showNotification; player removeEventHandler ["Fired", 0] };
```
### Blames Player, spawns Sandstorm on head.
```sqf
//Blames player (have to edit astrals with players name) then puts sandstorm on their head.
if(name player == "Astral")then{ } else { [] spawn {sleep 5; _BRG_popuptext = "<t size='1' color='#ff1111'>" + "WARNING Astral using SSPCM to cheat" + "</t>"; _BRG_popuptext2 = "<t size='1' color='#ff1111'>" + "Type in chat '#kick Astral' if want remove him in the game" + "</t>"; _BRG_value1 =[_BRG_popuptext,0.01,(safeZoneY + 0.05),0.5,0,0,90]spawn bis_fnc_dynamicText; playsound "Hint"; sleep 2; _BRG_value1 =[_BRG_popuptext,0.01,(safeZoneY + 0.05),0.5,0,0,90]spawn bis_fnc_dynamicText; sleep 2; _BRG_value1 =[_BRG_popuptext,0.01,(safeZoneY + 0.05),5,0,0,90]spawn bis_fnc_dynamicText; sleep 5; _BRG_value1 =[_BRG_popuptext2,0.01,(safeZoneY + 0.05),15,0,0,90]spawn bis_fnc_dynamicText; playsound "Hint"; }; };
puts a small sandstorm near player
[player, -1, 0.8, true] call BIS_fnc_sandstorm;
```
### Fabulous Purple Smoke.
```sqf
//Purple Smoke from player or players booty.
_expl1 = "Bo_GBU12_LGB" createVehicle position player; _expl1 attachTo [player, [-0.1, 0.1, 0.15], "Pelvis"]; _expl1 setVectorDirAndUp [ [0.5, 0.5, 0], [-0.5, 0.5, 0] ]; _expl2 = "Bo_GBU12_LGB" createVehicle position player; _expl2 attachTo [player, [0, 0.15, 0.15], "Pelvis"]; _expl2 setVectorDirAndUp [ [1, 0, 0], [0, 1, 0] ]; _expl3 = "Bo_GBU12_LGB" createVehicle position player; _expl3 attachTo [player, [0.1, 0.1, 0.15], "Pelvis"]; _expl3 setVectorDirAndUp [ [0.5, -0.5, 0], [0.5, 0.5, 0] ];
```
### SUPER EVIL COMMAND !!
```sqf
//SUPER EVIL COMMAND "Freeze players game"
disableUserinput true
```
