# Final BBO Results

This file summarises the final observed performance of the eight black-box functions after 13 optimisation rounds.

## Best observed results

| Function | Best observed output | Best round |
|---|---:|---:|
| Function 1 | 1.7124744581327652e-13 | 13 |
| Function 2 | 0.7567071185005707 | 12 |
| Function 3 | -0.02894866193240312 | 11 |
| Function 4 | 0.6097021692966149 | 13 |
| Function 5 | 4441.286859939468 | 13 |
| Function 6 | -0.2355946001700345 | 12 |
| Function 7 | 2.561618942565491 | 13 |
| Function 8 | 9.9971608560546 | 13 |

## Final Round 13 queries and outputs

| Function | Final query | Round 13 output |
|---|---|---:|
| Function 1 | `[0.714802, 0.733000]` | 1.7124744581327652e-13 |
| Function 2 | `[0.693778, 0.999999]` | 0.43684542751459654 |
| Function 3 | `[0.480004, 0.617171, 0.058672]` | -0.03303091950795441 |
| Function 4 | `[0.362916, 0.399525, 0.418896, 0.428926]` | 0.6097021692966149 |
| Function 5 | `[0.999999, 0.106000, 0.999999, 0.999999]` | 4441.286859939468 |
| Function 6 | `[0.448596, 0.293706, 0.701605, 0.756821, 0.000100]` | -0.24343477514566614 |
| Function 7 | `[0.177518, 0.189461, 0.450969, 0.168344, 0.372787, 0.766045]` | 2.561618942565491 |
| Function 8 | `[0.114846, 0.142684, 0.138612, 0.155654, 0.847573, 0.495220, 0.180066, 0.637573]` | 9.9971608560546 |

## Late-stage performance

Round 12 produced new best observations for six functions:

- Function 2
- Function 4
- Function 5
- Function 6
- Function 7
- Function 8

Round 13 produced new best observations for five functions:

- Function 1
- Function 4
- Function 5
- Function 7
- Function 8

The final two rounds were therefore the strongest part of the optimisation project.

## Key observations

Function 1 achieved its best result in the final round after testing the opposite side of a failed Round 12 local move.

Function 2 demonstrated an extremely sharp local optimum. A change of only 0.000001 improved the result substantially in Round 12, while another move of the same size in the same direction produced a much worse result in Round 13.

Function 5 became almost one-dimensional during late-stage optimisation, with three coordinates held close to the upper boundary while the second coordinate was refined.

Function 6 improved after simplifying the search to a single-coordinate perturbation.

Functions 7 and 8 responded well to continued local directional refinement.

These results supported the final function-specific optimisation strategy rather than using one common surrogate or acquisition rule for all eight functions.