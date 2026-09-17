# Week 07 Controls Lab — Responses

Answers and recorded model results from `submission.json`. This document does not recompute or independently validate the results.

## Submission status

- Schema: week07.submission/v1

- Record ID: c56f84d0-44af-47ec-81d0-ed0b0146e40d

- Record revision: 285

- Model hash: fnv1a-be327008

- Readiness: Marked ready by the submission.

## Supplied setup (instructor supplied)

### question — instructor supplied
Calculate required control moment, elevator moment, and the change with airspeed. Explain whether the nominal response meets +0.12 rad/s².

### system — instructor supplied
Illustrative planar pitch model. Aircraft geometry, integration, force conversion and constraints are supplied.

### representation — instructor supplied
Body axes forward/right/down. Positive pitch moment nose-up. Positive Fz downward. Positive elevator trailing edge down. Reference/CG X=0 m; tail X=-3 m.

### inputs — instructor supplied
Iy=5000 kg·m²; target=+0.12 rad/s²; competing=-750 N-m; density=1.225 kg/m³; V=40 m/s; S=16 m²; chord=1.5 m; Cmδ=-0.8/rad; elevator=-5°. Inputs are illustrative, not calibrated.

## Student responses

### physics
**Prompt:** Explain why a downward force aft of the CG gives a positive nose-up moment.

**Student response:**
```
A downward force behind the CG pushes the tail down, causing the nose to rotate upward. Since the sign convention defines nose up moment as positive, this produces a positive pitch moment.
```

### assumptions
**Prompt:** Explain one supplied assumption and what could invalidate it: planar motion, fixed reference, local linear effectiveness, no trim or damping.

**Student response:**
```
One assumption is that the elevator response is linear, meaning the change in pitching moment is proportional to the elevator angle. This may not be true at large elevator angles or near stall because the airflow becomes nonlinear.
```

### model
**Prompt:** Write your demand, dynamic-pressure, coefficient and moment equations. Identify which quantities are supplied and which are unknown.

**Student response:**
```
The demand model states that the control moment plus the competing moment must equal the moment needed to achieve the target pitch acceleration. Dynamic pressure depends on air density and the square of airspeed, while the elevator moment depends on dynamic pressure, wing area, chord, elevator effectiveness, and elevator angle. All of these values are supplied, while the required control moment and actual elevator moment are the values that need to be calculated.
```

### prediction
**Prompt:** Before running your own implementation, predict the sign of its elevator moment and the effect of halving airspeed. Explain the competing moment.

**Student response:**
```
I predict the elevator moment will be positive, meaning nose up, because the negative elevator angle and negative elevator effectiveness produce a positive moment. If the airspeed is halved, the elevator moment should become on quarter as large because it depends on the square of airspeed. The competing moment is negative, so it produces a nose down moment that the elevator must overcome.
```

### verification
**Prompt:** Show one independent hand calculation with units. Compare it with your model, and explain a sign, unit, or limiting-case check.

**Student response:**
```
q = 0.5pV^2

q = 0.5 × 1.225 kg/m^3 × (40 m/s)^2

q = 0.5 × 1.225 × 1600

q = 980 kg/(m·s^2)

q = 980 Pa

980 Pa, which matches the model result of 980 Pa. If the airspeed becomes zero, the dynamic pressure will also become zero, so the elevator will produce no aerodynamic moment.
```

### claim
**Prompt:** What do your computed results support at the stated condition? Include a limitation.

**Student response:**
```
The model gives an achieved pitch acceleration of 0.1784 rad/s^2, which is higher than the requested 0.12 rad/s^2. This means the -5 deg elevator produces more nose-up moment than required at 40 m/s. One limitation is that the model assumes a linear elevator response and does not include aerodynamic damping or trim.
```

### reflection
**Prompt:** What additional evidence or missing physics would you investigate next?

**Student response:**
```
I would investigate how aerodynamic damping and trim affect the pitch response. I would also test different airspeeds and elevator angles to see when my linear assumption starts to become inaccurate.
```

### AI use
**Prompt:** Identify the AI tool and how you used it, what you changed, and how you independently checked the result. State “No AI used” if applicable.

**Student response:**
```
I used ChatGPT to help me understand the equations and create the structured JSON expressions, as some of the instructions were confusing to me. I changed the explanations to match my own understanding and the results I observed. I independently checked the dynamic pressure by hand using 0.5 x 1.225 x 40^2 = 980 Pa, which matched the model result. I also used ChatGPT to help fix my grammar and English after writing my responses, without changing the engineering content of my work.
```

## Equations and model source

The recorded model JSON/expression source follows exactly as supplied. It is not interpreted or recomputed here.

```
{
  "schemaVersion": "week07.student-model/v1",
  "id": "week07-controls-model",
  "version": "1.0.0",
  "slots": [
    {
      "id": "controls.demand",
      "expressions": [
        {
          "name": "requiredMoment",
          "expression": "pitchInertia * requestedAcceleration - competingMoment",
          "unit": "N*m"
        }
      ]
    },
    {
      "id": "controls.effectiveness",
      "expressions": [
        {
          "name": "dynamicPressure",
          "expression": "0.5 * density * airspeed * airspeed",
          "unit": "Pa"
        },
        {
          "name": "deltaCm",
          "expression": "elevatorDerivative * elevatorAngle",
          "unit": "1"
        },
        {
          "name": "deltaMoment",
          "expression": "dynamicPressure * referenceArea * referenceChord * deltaCm",
          "unit": "N*m"
        }
      ]
    }
  ]
}
```

## Recorded verification status

Recorded as passed for the submitted model hash.

- Checked at: 2026-09-17T03:59:37.012Z
- Detail: Student artifact passed demand, baseline elevator, quadratic speed, and neutral-deflection checks.

## Recorded model runs

### Run 1
- Recorded: 2026-09-17T03:59:35.413Z
- Run ID: 39bb0cfe-b589-43db-835e-84dff9a6c47b
- Record revision: 23
- Model hash recorded with run: fnv1a-be327008
- Prediction recorded with run:

```
I predict the elevator moment will be positive, meaning nose up, because the negative elevator angle and negative elevator effectiveness produce a positive moment. If the airspeed is halved, the elevator moment should become on quarter as large because it depends on the square of airspeed. The competing moment is negative, so it produces a nose down moment that the elevator must overcome.
```
- Result status: recorded values shown below
- Values: `requiredMoment=1350 N*m`; `dynamicPressure=980 Pa`; `deltaCm=0.06981317007977318 1`; `deltaMoment=1642.0057602762652 N*m`

### Run 2
- Recorded: 2026-09-17T03:59:38.940Z
- Run ID: 039bd81a-e0bd-4487-9e0c-9f435e2a5cd6
- Record revision: 23
- Model hash recorded with run: fnv1a-be327008
- Prediction recorded with run:

```
I predict the elevator moment will be positive, meaning nose up, because the negative elevator angle and negative elevator effectiveness produce a positive moment. If the airspeed is halved, the elevator moment should become on quarter as large because it depends on the square of airspeed. The competing moment is negative, so it produces a nose down moment that the elevator must overcome.
```
- Result status: recorded values shown below
- Values: `requiredMoment=1350 N*m`; `dynamicPressure=980 Pa`; `deltaCm=0.06981317007977318 1`; `deltaMoment=1642.0057602762652 N*m`

## Submission instructions

Use Save to GitHub in the app to save both files, commit, and push. Submit your fork URL and the saved commit SHA. Manual fallback: save this file beside `student/submission.json`, run `npm run student:prepare` and `npm run student:validate`, then commit and push student/.
