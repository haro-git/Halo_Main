<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1120,45:1E3A5F,100:F59E0B&height=190&section=header&text=Halo&fontSize=64&fontColor=FFFFFF&fontAlignY=34&desc=Building%20an%20AGI%20humanoid%20%E2%80%94%20one%20subsystem%20at%20a%20time&descAlignY=54&descSize=15" width="100%" alt="banner"/>

<img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=19&pause=1200&color=F59E0B&center=true&vCenter=true&width=700&lines=Goal%3A+an+AGI+humanoid.;Currently+building+one+of+its+parts+%E2%80%94+the+hand.;Calculate+a+hypothesis.+Build+it.+Measure+where+it+was+wrong." alt="typing"/>

<br/>

<a href="mailto:submin47@gmail.com"><img src="https://img.shields.io/badge/Email-submin47@gmail.com-F59E0B?style=for-the-badge&logo=gmail&logoColor=white" alt="email"/></a>
<img src="https://img.shields.io/badge/Goal-AGI%20Humanoid-1E3A5F?style=for-the-badge" alt="goal"/>
<img src="https://img.shields.io/badge/Now-The%20Hand-D97706?style=for-the-badge" alt="now"/>
<img src="https://komarev.com/ghpvc/?username=haro-git&style=for-the-badge&color=0B1120&label=PROFILE+VIEWS" alt="views"/>

</div>

---

## 👋 About

**I want to build an AGI humanoid.** That is the whole goal. Everything on this profile is one
subsystem of it.

Right now I'm building **the hand** — because a general-purpose body is worth very little without a
general-purpose end effector, and because the hand is where the hard problems concentrate: eleven
joints, tendon routing, and contact you cannot fake in simulation.

Two months in I had a tendon-driven hand assembled — then swapped out the actuator the BOM called
for, which meant redesigning the power rail and re-deriving a good deal of what was never published.
Most of my work is that loop: **make a number, build the thing, then find out where the number was
wrong.**

Self-taught, working through the stack one subsystem at a time.

<br/>

## 🔧 Currently Building — ORCA Hand Lite

> A tendon-driven robotic hand. The Lite variant is only partially open-sourced, so assembly, tendon
> routing, servo wiring, bus configuration and calibration all had to be reconstructed from the CAD.
> Built together with two other engineers I met in the ORCA Hand Discord.

**⚡ Actuator & power redesign**

Replaced the BOM's Feetech STS3215 with a different servo, which meant the electrical side had to be
redone rather than adapted.

- 12 V → **5 V rail redesigned** from scratch
- Multi-channel supply re-sized against **1.47 A stall per axis**
- Fingertip force estimated from stall and rated torque, spool radius and joint moment arm

**Predicted bottleneck: not torque — heat at stall-hold.** A hand spends its life gripping near
stall, so the limit is thermal rather than mechanical. Instrumenting current and temperature to
confirm.

**🔩 Reconstructed from the CAD**

Nothing about the Lite build order was published. Assembly sequence, tendon routing, servo wiring,
bus configuration and calibration each had to be inferred from the geometry, checked against the
official kinematics, and then written up so the two people building alongside me were not solving it
a second time.

Everything gets derived from the model and verified against it — exact solid classification on the
CAD rather than mesh approximation, watertightness checks on every generated part, and a full
right-hand physics model to confirm travel before anything is printed.

**❓ Still unmeasured — needs real hardware:** joint friction, and how far the servos drift once they
have been holding a grip for a while. Neither shows up in simulation; both decide whether the hand
is usable.

<br/>

## 🛣️ Up next — Sim-to-Real with Isaac Sim

The hand already runs in MuJoCo. The next step is **NVIDIA Isaac Sim / Isaac Lab**: train grasping
policies in simulation and close the loop on the physical hand.

The parts I expect to be hard are exactly the ones I have not measured yet:

- **Tendon friction and hysteresis** — the sim assumes an ideal return. The real hand loses travel every cycle to friction, and that loss has to be identified on hardware and fed back into the model.
- **Thermal drift at stall-hold** — a policy trained on a servo that never heats up will not survive a hand that grips for thirty seconds.
- **Actuator model fidelity** — current-based position control does not behave like an idealised torque source.

Same loop as everything else here: **model it, run it, then measure where the model was wrong.**

<br/>

## 📐 How I work

```mermaid
flowchart LR
    A(["hypothesis"]) --> B["calculate"]
    B --> C["build"]
    C --> D["measure"]
    D --> E{"does it<br/>match?"}
    E -- "no" --> F["find where<br/>it broke"]
    F --> A
    E -- "yes" --> G(["next unknown"])
    G --> A

    style A fill:#F59E0B,stroke:#B45309,color:#0B1120
    style G fill:#1E3A5F,stroke:#F59E0B,color:#FFFFFF
    style F fill:#7C2D12,stroke:#F59E0B,color:#FFFFFF
```

- **Numbers before parts.** Stall current, moment arms and stress ratios get computed before anything is ordered.
- **Derive, don't assume.** Joint mapping, routing paths and clearances all came out of the CAD geometry rather than a guess.
- **Write down what is still wrong.** Everything I publish carries a "not yet verified" section, and revisions say why they happened.

<br/>

## 🧰 Toolbox

<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://skillicons.dev/icons?i=python,ros,ubuntu,raspberrypi,blender,git,linux,bash&theme=dark"/>
  <img src="https://skillicons.dev/icons?i=python,ros,ubuntu,raspberrypi,blender,git,linux,bash&theme=light" alt="python, ros 2, ubuntu, raspberry pi, blender, git, linux, bash"/>
</picture>

<br/><br/>

**Robotics & Control**

<img src="https://img.shields.io/badge/DYNAMIXEL%20SDK-1E3A5F?style=for-the-badge" alt="dynamixel sdk"/>
<img src="https://img.shields.io/badge/Protocol%202.0%20%2F%20TTL%20bus-1E3A5F?style=for-the-badge" alt="protocol 2.0"/>

**Simulation & Sim-to-Real**

<img src="https://img.shields.io/badge/NVIDIA%20Isaac%20Sim-76B900?style=for-the-badge&logo=nvidia&logoColor=white" alt="isaac sim"/>
<img src="https://img.shields.io/badge/Isaac%20Lab-76B900?style=for-the-badge&logo=nvidia&logoColor=white" alt="isaac lab"/>
<img src="https://img.shields.io/badge/MuJoCo-1E3A5F?style=for-the-badge" alt="mujoco"/>
<img src="https://img.shields.io/badge/Sim--to--Real-D97706?style=for-the-badge" alt="sim to real"/>

**CAD & Fabrication**

<img src="https://img.shields.io/badge/Autodesk%20Fusion-F58220?style=for-the-badge&logo=autodesk&logoColor=white" alt="autodesk fusion"/>
<img src="https://img.shields.io/badge/STEP%20%2F%20OpenCascade-0B1120?style=for-the-badge" alt="opencascade"/>
<img src="https://img.shields.io/badge/trimesh-4B8BBE?style=for-the-badge" alt="trimesh"/>
<img src="https://img.shields.io/badge/FDM%20%2F%20SLA%20printing-6E7681?style=for-the-badge" alt="printing"/>
<img src="https://img.shields.io/badge/Tendon%20routing-D97706?style=for-the-badge" alt="tendon routing"/>

**Certified & hands-on**

<img src="https://img.shields.io/badge/Craftsman%20Electricity-1E3A5F?style=for-the-badge" alt="craftsman electricity"/>
<img src="https://img.shields.io/badge/Wiring%20%C2%B7%20Termination%20%C2%B7%20Insulation-0B1120?style=for-the-badge" alt="wiring, termination, insulation"/>

</div>

<br/>

## 📫 Reach me

<div align="center">

<a href="mailto:submin47@gmail.com"><img src="https://img.shields.io/badge/Email-submin47@gmail.com-F59E0B?style=for-the-badge&logo=gmail&logoColor=white" alt="email"/></a>
<a href="https://github.com/haro-git?tab=repositories"><img src="https://img.shields.io/badge/Repositories-0B1120?style=for-the-badge&logo=github&logoColor=white" alt="repositories"/></a>

<br/><br/>

<em>Short on credentials. Long on iterations.<br/>Building toward a humanoid, one measured subsystem at a time.</em>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:F59E0B,55:1E3A5F,100:0B1120&height=110&section=footer" width="100%" alt="footer"/>

</div>
