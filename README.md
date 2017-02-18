# arma3-debug-commands
Usable debug commands for server admins

### Disable fatique (without ACE loaded)

```sqf
// DISABLE NOW
player enableFatigue false;
// DISABLE AFTER RESPAWN
player addEventhandler ["Respawn", {player enableFatigue false}];
```
