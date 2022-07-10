# kOS processor options for mods

The *Embedded kOS Kirkuits* modlet defines a number of different processor options that can be easily added to a part by just setting the `Embedded_kOSProcessor_type` entry to the corresponding value in a MM patch that executes `BEFORE[EmbeddedKOSKirkuits]`. 

The `Embedded_kOSProcessor_type` can be present either in a `PART`, a `MODULE[kOSProcessor]` or in an `UPGRADE` node. In the latter two cases, the kOSProcessor specific values will be set (or changed) to the values defined by the processor type setting. 

Another setting `Embedded_kOSProcessor_include` (which can only be set on a `PART` node) controls whether the kOSProcessor module is 

* always added to the part (value `always`)
* added to the part but can be disabled via PAW in the VAB/SPH if B9PArtSwitch is 
  installed (`optional_default_on`)
* can be included via PAW but is off by default (`optional_default_off`).
* is never included (`never`).

The `optional_default_on` and `optional_default_off` settings require B9PartSwitch to provide the 
actual on/off switch via PAW. If B9PartSwitch is not installed, `optional_default_on` is handled 
identically to `always`,  and `optional_default_off` identical to `never`. And `never` can be used 
to explicitly mark parts that should not get an optional kOSProcessor module.

Examples:
```
// Include an optional kOSProcessor on myProbeCore
@PART[myProbeCore]:NEEDS[EmbeddedKOSKirkuits] {
    %Embedded_kOSProcessor_type = modern_small
    %Embedded_kOSProcessor_include = optional_default_on
}

// Add a "default" type kOSProcessor to myLargerProbeCore that can later be upgraded to
// a "modern_medium" processor
@PART[myProbeCore]:NEEDS[EmbeddedKOSKirkuits] {
   MODULE[kOSProcessor] {
       Embedded_kOSProcessor_type = default
       UPGRADES {
           UPGRADE {
               name__ = kOSProcessorUpgrade_1
               techRequired__ = miniaturization
               Embedded_kOSProcessor_type = modern_medium 
           }
       }
   }
}
```

## processor option `early_basic`

This option defines a kOS processor that is comparably heavy, has very little permanent memory 
("disk space" in kOS parlance), uses a lot of electricity to run and costs quite a bit of funds. 
Corresponds conceptually to early guidance systems, but this is a pretty loose match because it 
is a programmable digital computer which almost all of the real-world early guidance systems 
were not.

In-game, this is the option for early in the tech tree, and it has by design too little storage 
space for more than the simplest flight scripts (in-game inspiration for this is the kOS processor 
on the USI sounding rockets probe cores).

### processor option `early_advanced`

This option is similar to the `early_basic` option, but has more storage space - at the cost of 
increased mass, price and electricity consumption. Corresponds to early digital guidance computers
in real life (think [Apollo Guidance Computer](https://en.wikipedia.org/wiki/Apollo_Guidance_Computer).

### processor option `default`

This is the mainstream, standard option and has the same price, disk space and resource 
consumption to the "KR-2042 b Scriptable Control System", but a little less mass. The default
configuration for this option is actually called the "KR-2042 e Scriptable Core" to reflect this,
and can be thought of as an "KR-2042 b" stripped of its blinkenlights and housing and installed 
directly into a probe core.

All of the "early" options have less storage, consume more resources and are more expensive, and at least the `early_advanced` option has more mass as well. 

Think "1990s era flight computers" for the real-world role model.

### processor option `modern_small`

This option defines a small and cheap processor with very low resource needs but not much storage space.
Think "modern micro controller". 

Storage space is roughly comparable to the `early_advanced` option as a challenge for the player, 
but resource usage and price is negligible to make the challenge attractive.

### processor option `modern_medium`

This option is a bit more expensive than the `modern_small` option and needs a bit more electricity, 
but has considerably more storage space. Think "contemporary small to medium embedded computer" for the 
real-world inspiration. 

In-game, this is comparable to the `default` option in terms of storage space, but is cheaper and uses 
less electricity. This is the go-to option for most computing needs in the middle of the tech tree.

### processor option `modern_large`

This option is more expensive and a bit heavier than the `modern_medium` option and needs some more 
electricity as well, but has basically unlimited storage space.  Think "powerful contemporary computer" for the real-world inspiration. 

In-game, the mid-tech-tree option for advanced tasks when a single `modern_medium` part is not enough.

### processor option `unlimited`

Exactly what the option name says. Basically unlimited storage, and negligible cost and resource usage. 

This is the late-tech-tree future option where you no longer have to think about computing resources
because computing has become ubiquitous.
