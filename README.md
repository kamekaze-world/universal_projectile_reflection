# Universal Projectile Reflect 1.0
###### FOR IKEMEN GO Nightly 7/30/25 OR LATER

## Instructions

This plug and play armor works by the player 
turning the map "k_reflecting" on, once it is on
it will activate any attack that has this map set to 1 or higher
will reflect any helper or projectile that is trying to actively attack
it.

### Modifying your helper/projectile to be unreflectable

If you want to assert that your projectile or helper cannot be reflected you
need to set the sysvar(1) for the helper to a non zero value and for helpers
or add const(bit16) to your projectile id when its spawned. **If your helper 
uses projectiles for priority shields you must do both of these things. Also, 
your helper must be using projectile hit attributes or it will get ignored aka NP,SP,HP,AP **

EG for helpers in cns
```
[state 0]
type = varset
trigger1=time=0
sysvar(1)=1 ; i will not be reflected unless I change this value to 0
```
**Zss:**
```
if time=0{
sysvar(1):=1; #i will not be reflected unless I change this value to 0
}
```

EG for projectiles in cns
```
[State 1005, This is for fossils]
type = Projectile
trigger1 = time = 0
ProjID = 999+const(bit16) ;adding the const makes it unable to be reflected
```

**Zss:**

```
if time=0{
projectile{projid:999+const(bit16);otherstuff;}
}
```


### Modifying the player/helper to reflect

Make sure the animation you are using has a clsn1 defined and that you safeguard the state so that it doesn't get hit too early.
In the state of the helper/player you simply set the k_reflecting map to anything other than 0. When you want to stop reflecting you 
set it back to 0.
