# Week 07 Controls Lab — Responses

Answers and recorded model results from `submission.json`. This document does not recompute or independently validate the results.

## Submission status

- Schema: week07.submission/v1

- Record ID: c56f84d0-44af-47ec-81d0-ed0b0146e40d

- Record revision: 17

- Model hash: fnv1a-adee3cf8

- Readiness: Marked incomplete or not ready; missing: verification, claim, reflection, aiUse, execution

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
_Missing — no response supplied._

### claim
**Prompt:** What do your computed results support at the stated condition? Include a limitation.

**Student response:**
_Missing — no response supplied._

### reflection
**Prompt:** What additional evidence or missing physics would you investigate next?

**Student response:**
_Missing — no response supplied._

### AI use
**Prompt:** Identify the AI tool and how you used it, what you changed, and how you independently checked the result. State “No AI used” if applicable.

**Student response:**
_Missing — no response supplied._

## Equations and model source

The recorded model JSON/expression source follows exactly as supplied. It is not interpreted or recomputed here.

```
{
  "schemaVersion": "week07.student-model/v1",
  "id": "week07-student-model",
  "version": "1.0.0",
  "slots": [
    {
      "id": "controls.demand",
      "expressions": [
        {
          "name": "requiredMoment",
          "expression": "",
          "unit": "N*m"
        }
      ]
    },
    {
      "id": "controls.effectiveness",
      "expressions": [
        {
          "name": "dynamicPressure",
          "expression": "",
          "unit": "Pa"
        },
        {
          "name": "deltaCm",
          "expression": "",
          "unit": "1"
        },
        {
          "name": "deltaMoment",
          "expression": "",
          "unit": "N*m"
        }
      ]
    }
  ]
}
```

## Recorded verification status

No verification record was supplied.

## Recorded model runs

_Missing — no model runs supplied._

## Submission instructions

Use Save to GitHub in the app to save both files, commit, and push. Submit your fork URL and the saved commit SHA. Manual fallback: save this file beside `student/submission.json`, run `npm run student:prepare` and `npm run student:validate`, then commit and push student/.
