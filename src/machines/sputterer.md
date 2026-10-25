# Sputterer

## What is a sputterer?

The sputterer is a physical vapor deposition (PVD) tool. It uses a plasma to knock
atoms away from a *target* material and deposit them as a thin film on a *substrate*. 
Our goal building this machine is to deposit aluminum metallization layers and bulk
dielectric oxides such as aluminum oxide.

> **Build Status:** This machine is in active design and construction. Numbers, procedures, and the bill
> of materials below are working estimates and will change as the build matures.

## How sputtering works

A chamber is pumped down to vacuum and then back-filled with a low pressure of
process gas, usually argon. A large voltage between the target (cathode) and the
chamber or an anode ignites the gas into a plasma. Positive gas ions are
accelerated into the target and transfer their momentum to surface atoms, ejecting
them. The ejected target atoms condense on the substrate, building a thin film.

Most sputter sources are **magnetrons**: 

A magnetron is a device which uses permanent magnets behind the source to trap
electrons in a region close to the surface of the target. Doing this increases
the ionization rate, and lets the machine run at a lower pressure for a higher 
deposition rate

### Process variants

- **DC sputtering:**  a constant target voltage. Simple and effective for
  conductive targets such as aluminum.
- **RF sputtering:** the target potential alternates back and forth
  (commonly at 13.56 MHz). Reversing the polarity bleeds off the surface charge 
  that would otherwise build up on an insulating target. An RF power source is 
  required to sputter dielectrics such as aluminum oxide.
- **Reactive sputtering:** a reactive gas (oxygen, nitrogen) is added to the inert
  argon. The reactive gas combines with the sputtered metal to grow a compound
  film such as an oxide or nitride. In this configuration, the metal target
  produces a dielectric thin film layer instead of a metal one.

## Target specifications

- Deposit aluminum metallization layers.
- Deposit bulk dielectric oxides (e.g. aluminum oxide) via RF and/or reactive
  sputtering.

<!-- ## Major subsystems -->
<!---->
<!-- | Subsystem | Purpose | -->
<!-- |-----------|---------| -->
<!-- | Vacuum chamber | Holds the process at low pressure; must be clean and low-outgassing | -->
<!-- | Vacuum pumps | Rough pump plus a high-vacuum stage to reach base pressure | -->
<!-- | Sputter gun / magnetron | Holds and cools the target, contains the magnets | -->
<!-- | Power supply | High-voltage DC or RF drive for the plasma | -->
<!-- | Gas delivery | Argon and oxygen supply with a mass flow controller (MFC) | -->
<!-- | Cooling | Water cooling for the sputter gun | -->
<!-- | Shutter | Blocks the substrate until the plasma is stable and the target is clean | -->
<!-- | Substrate stage | Positions the wafer; may be heated in later revisions | -->

### Gas delivery

Gas flow is set with a **mass flow controller**. A rotameter (indicator-ball)
flow meter is a low-cost option; a digital MFC is more accurate and repeatable.
The system needs argon for the main process and oxygen for reactive/RF oxide
deposition. Gas control, storage, and exhaust routing require sign-off from the
facility (MNC) and the faculty advisor.

### Cooling

The sputter gun must be actively cooled. Ion bombardment dumps significant power
into the target, and an overheated target or bonded target backing can crack or
delaminate.

## Basic operation

1. Load the substrate. Clean the chamber interior first if needed (acetone wipe).
2. Close the shutter.
3. Pump down to base pressure.
4. Optionally perform an **argon flush** — flow argon and pump it away one or more
   times to purge adsorbed contaminants before the real run.
5. Set the process gas flow and chamber pressure with the MFC and throttle.
6. Ramp up the power supply and ignite the plasma.
7. Let the plasma stabilize and **pre-sputter** with the shutter closed to clean
   the target surface.
8. Open the shutter to deposit for the timed run.
9. Close the shutter, ramp down power, stop the gas, and vent the chamber to
   unload.

## Design considerations

**Outgassing** is the dominant design constraint. Every internal material slowly
releases adsorbed gas under vacuum, which limits base pressure and contaminates
the film.

- No plastics inside the vacuum space.
- No brass — the zinc evaporates out of the alloy under vacuum.
- Gaskets: **Viton** (fluoroelastomer). We still need to source a vendor who can
  laser-cut Viton sheet to our gasket profiles.

## Safety

- **High voltage.** The plasma supply is high, ionizing voltage. All supplies must
  have grounded shielding and no touchable contacts. High voltage or high current
  can be derived from microwave-oven transformers; transformers are dangerous and
  must be treated with respect. (For contrast, a thermal evaporator is a
  high-*current* tool; the sputterer is a high-*voltage* tool.)
- **Gases.** Secure all cylinders. Fit pressure-relief protection and prevent
  over-pressurization. Even inert argon can asphyxiate in a confined space, and an
  oxygen-enriched atmosphere is a severe fire and combustion hazard. Install
  detectors for hazardous gases. Exhaust routing needs facility input.
- **Implosion.** Any glass under vacuum can implode, especially while it is being
  modified. If you hear a crack, look away and duck.
- **Contamination and particulates.** Clean the chamber regularly. Only use tested,
  verified targets and gases — avoid hazardous target chemistries (e.g.
  beryllium). Do not blow parts clean; that aerosolizes metal flakes. Wear a mask
  when cleaning.
- **Machining.** Fabricating the vacuum parts uses heavy machine-shop equipment.

<!-- ## Cost estimate -->
<!---->
<!-- Roughly **\$7,800–\$18,400**, scaled from the Hacker Fab RF sputtering chamber -->
<!-- design and its bill of materials. -->

## References and background

- Hacker Fab — DIY RF sputtering chamber:
  <https://docs.hackerfab.org/home/fab-toolkit/deposition/diy-rf-sputtering-chamber>
- The Thought Emporium — sputtering system:
  <https://www.youtube.com/watch?v=aljbjJbfghs> ·
  <https://github.com/thethoughtemporium/sputteringsystem>
- Applied Science (Ben Krasnow) — intro to the sputtering process:
  <https://benkrasnow.blogspot.com/2013/11/intro-to-sputtering-process-to-create.html>
  and
  <https://benkrasnow.blogspot.com/2013/12/more-info-about-sputtering-process.html>
- Hackaday — practical plasma for thin-film deposition:
  <https://hackaday.com/2018/04/11/practical-plasma-for-thin-film-deposition/>
- Hackaday.io — sputtering magnetron project:
  <https://hackaday.io/project/188141-sputtering-magnetron>
- Overview video: <https://www.youtube.com/watch?v=L6ZIkmIVm6c>

---

*Questions? Ask in the Minnesota Nano Fab Club channel.*
