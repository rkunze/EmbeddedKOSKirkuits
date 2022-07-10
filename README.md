# Embedded kOS Kirkuits
This modlet defines a number of different kOS processor options that can be easily added to a part by a MM patch.

Dependencies are pretty minimal:
* required: _kOS_ and _Module Manager_
* recommended: _B9 Part Switch_

_Embedded kOS Kirkuits_ will work without _B9 Part Switch_, but with _B9 Part Switch_ installed you get the option to select or deselect the embedded kOS processor om a probe core in the VAB.

The intention of this mod is to add different processor options to probe cores and command modules depending on where they are unlocked in the tech tree, which means it needs dedicated support for each tech tree. Out of the box, *Embedded kOS Kirkuits* supports these tech trees:
* [The Skyhawk Science System](https://forum.kerbalspaceprogram.com/index.php?/topic/206109-the-skyhawk-science-system-a-new-realistic-tech-tree-for-ksp-now-including-kerbalism-support-v110-for-science-62822/)

I will probably not add support for more than that myself (because I mainly wrote *Embedded kOS Kirkuits* to support my current career mode play which uses the Skyhawk Science System), but I am happy to accept pull requests to add support for other mods. If you are interested on adding *Embedded kOS Kirkuits* support to a mod, see [kOS processor options for mods](processors.md) for instructions and `ModSupport/SkyhawkScienceSystem.cfg` for an example configuration that supports a tech tree mod.

By default, _Embedded kOS Kirkuits_ does nothing to parts that are not explicitly configured to use _Embedded kOS Kirkuits_. If you want to have it act like "kOS for All!" instead and just slap a kOS processor onto everything that has no explicit configuration, there is a (deactivated) example patch in `ModSupport/kOSforAll.cfg.example` which does exactly that.

## Installation

At the moment, only a development version is available. The recommended way to install is to
directly clone the GitHub repository in your `GameData` directory:
~~~ sh
cd $KSP_DIR/GameData
git clone https://github.com/rkunze/EmbeddedKOSKirkuits.git
~~~

This requires that you have [Git](https://git-scm.com/) installed on your computer, but allows to update _Embedded kOS Kirkuits_ later on with a simple `git pull`. 

As an alternative if you do not have Git, [download the current development status](https://github.com/rkunze/EmbeddedKOSKirkuits/archive/refs/heads/main.zip), unpack the zip file within your `GameData` directory, and rename `GameData/EmbeddedKOSKirkuits-main` to `GameData/EmbeddedKOSKirkuits`. For updates, you need to delete the `GameData/EmbeddedKOSKirkuits` directory and reinstall from scratch.