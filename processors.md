# kOS processor options for mods

The *Embedded kOS Kirkuits* modlet defines a number of different processor options that can be easily added to a part by just setting the `EmbeddedKOSProcessorType` entry to the corresponding value in a MM patch that executes before `LAST[EmbeddedKOSKirkuits]`.

The `EmbeddedKOSProcessorType` can be present either in a `PART`, a `MODULE[kOSProcessor]`, or an `UPGRADE` node. In the latter two cases, the kOSProcessor specific values will be set (or changed) to the values defined by the processor type setting.

Another setting `EmbeddedKOSProcessorInclude` (which can only be set on a `PART` node) controls whether the kOSProcessor module is

* always added to the part (value `always`)
* added to the part if it will fit into the mass and cost budget of the part (value `if_in_budget`, see below for details)
* is never included (`never`).

if `EmbeddedKOSProcessorInclude` is `if_in_budget`, the specified processor core is only included if it
fits within the mass and cost budget of the part. The mass budget for a processor option is specified by the `baseModuleMass` and `massBudgetFactor` of the corresponding `EMBEDDED_KOS_KIRKUITS/PROCESSOR` node. The embedded kOS processor will fit into the mass budget of a part if `baseModuleMass * massBudgetFactor` is not greater than the total mass of the part. Cost budget works the same way, but uses `baseModuleCost` and `costBudgetFactor`.

Examples:
```
// Include the most powerful kOSProcessor on myProbeCore that the mass and cost budget allows.
@PART[myProbeCore]:NEEDS[EmbeddedKOSKirkuits] {
    EmbeddedKOSProcessorType = modern_large
    EmbeddedKOSProcessorType = modern_medium
    EmbeddedKOSProcessorType = modern_small
    EmbeddedKOSProcessorInclude = best_fit
}

// Add a "default" type kOSProcessor to myLargerProbeCore that can later be upgraded to
// a "modern_medium" processor
@PART[myProbeCore]:NEEDS[EmbeddedKOSKirkuits] {
   MODULE[kOSProcessor] {
       EmbeddedKOSProcessorType = default
       UPGRADE {
           name__ = modern_processors
           EmbeddedKOSProcessorType = modern_medium
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
consumption to the "KR-2042 b Scriptable Control System", but less mass. Can be thought
of as an "KR-2042 b" stripped of its blinkenlights and housing and installed
directly into a probe core.

All of the "early" options have less storage, consume more resources and are more expensive, and at least the `early_advanced` option has more mass as well.

Think "1990s era flight computers" for the real-world role model.

### processor option `advanced`

Another mid-game option, this time modeled after the "CX-4181 Scriptable Control System".

Think "1990s era flight computers" for the real-world role model.

### processor option `modern_small`

This option defines a small and cheap processor with very low resource needs but not much storage space.
Think "modern micro controller".

Storage space is just a bit more than the `early_basic` option as a challenge for the player,
but resource usage and price is negligible to make the challenge attractive.

### processor option `modern_medium`

This option is a bit more expensive than the `modern_small` option and needs a bit more electricity,
but has considerably more storage space. Think "contemporary small to medium embedded computer" for the
real-world inspiration.

In-game, this is comparable to the `default` option in terms of storage space, but is cheaper and uses
less electricity. This is the go-to option for most computing needs in the last third of the tech tree.

### processor option `modern_large`

This option is more expensive and a bit heavier than the `modern_medium` option and needs some more
electricity as well, but has basically unlimited storage space.  Think "powerful contemporary computer" for the real-world inspiration.

In-game, the option for advanced ships in last third of the tech tree when a single `modern_medium` part is not enough.

### processor option `unlimited`

Exactly what the option name says. Basically unlimited storage, and negligible cost and resource usage.

This is the late-tech-tree future option where you no longer have to think about computing resources
because computing has become ubiquitous.
