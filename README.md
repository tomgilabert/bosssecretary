### bosssecretary module for FreePBX

The boss-secretary module creates a special **ring group** which includes
one or more "bosses" and one or more secretaries". When someone calls
the boss' extension, the secretary (or secretaries) extension will ring only, 
allowing the secretary to answer his or her boss' call.

Additionally, you can define one or more chief extensions, 
who may call boss extension directly without ringing the secretary's extension.

The module includes codes for activating (*153), deactivating(*153) and
toggling(*152) the groups' state. For example, when a secretary ends her working day, she
may turn off the boss-secretary group by dialing *152+`<ext number>`, so her
boss will receive calls directly.

The module generates the appropriate hints to have ip phones show the
groups state by subscribing to the *152+`<ext number>` extension (context:`
app-bosssecretary-hints`). 
You can set this functionality to blf button on your phone.

For example for Linksys/ Cisco phones:

```
fnc=blf+sd;sub=*152EXT@$PROXY;ext=*152@PROXY
```

Or chan_sccp for a secretry using extension 9999:
```
button = speeddial, *152, ToggleBossSecretary, *1529999@app-bosssecretary-hints
```

Use of 'silent_ring'
------
You can create a line button on the bosses phone using
```
button = line, 1234, bossman !silent
```
And check the "Ring boss(es) silently" checkbox. Bosses will see an incoming
call on the phone but it will not ring. However when another boss, secretary
or chief calls the phone will ring.
