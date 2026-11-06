# EGM eyewear reviewers

Specialist reviewer prompts for designing a physical product, spectacle frames, with Google's [Elephant-Goldfish Model](https://github.com/google/elephant-goldfish-model) (EGM).

EGM's rule is: design with an elephant, review with a goldfish. The elephant is one agent that holds the whole conversation and writes the design doc. The goldfish are fresh agents that read only the doc, so anything said but never written down shows up as a gap. EGM's stock goldfish are written for software. This repo replaces them with reviewers who know eyewear.

These prompts come from three experimental runs in which agents designed a pair of glasses from a one-line brief, and a builder agent made each version in Blender from the doc alone. They are one experiment's prompts, not a tested product.

## The reviewers

| Reviewer | Question it answers | What it sees |
|---|---|---|
| [Optician](reviewers/optician.md) | Does it fit and sit right on a real face? | Doc, then front, inside, top, side and under views |
| [Frame Maker](reviewers/frame-maker.md) | Can it be made and assembled? | Doc, then three-quarter, inside, top, under and hinge views |
| [Hinge Engineer](reviewers/hinge-engineer.md) | Do the moving parts work and survive use? | Doc, then hinge close-ups and folded views |
| [Materials and Finish](reviewers/materials-finish.md) | Does each surface read as its real material, and can it be made? | Doc, then lit renders with materials |
| [Art Director](reviewers/art-director.md) | How does it look and feel? | Renders only, no brief |
| [Cold Viewer](reviewers/cold-viewer.md) | What does a stranger think this is? | One render, nothing else |

EGM's stock `implementation_readiness` goldfish stayed in, with one added line: the implementer builds 3D glasses in Blender rather than writing code, and it also reads the builder's list of guesses, since every guess marks a gap in the doc.

## Rules that made them work

- **Stay in your lane.** Each specialist raises findings only in its own area.
- **Source every number, or say unknown.** A specialist that invents a standard sounds expert and is wrong.
- **Show each reviewer only the views it needs.** Gray, untextured renders for shape; lit renders with materials only for the reviewers who judge surfaces.
- **Keep taste with the owner.** Reviewers flag; the owner decides matters of taste, by picking between drawings rather than describing what they want.
- **Neutral wording.** An early version of these prompts named the problems we expected, and the reviewers found exactly those. Describe the job, not the answer.

## What changed

| | Stock software reviewers | These specialists |
|---|---|---|
| Example finding | A missing README file | Nose pad contact area, wall thickness around the lens, how the hinge pin is retained |

The specialists raised findings about real glasses. They did not make the list converge on their own; the owner's either-or picks did more for that than extra rounds.

## How to use

Put the files in `reviewers/` wherever your EGM setup loads goldfish personas, or pass a file's text as the reviewer's system prompt. The four specialists follow EGM's persona format and run in `Mode: REVIEW`. The Art Director and Cold Viewer are plain prompts.

To adapt them to another product, keep the structure (role, the one question, what to check, source-or-unknown) and rewrite the role for the trade that knows that product.

## License and credit

Apache License 2.0, see [LICENSE](LICENSE). The four specialist prompts are adapted from the goldfish persona files in Google's [elephant-goldfish-model](https://github.com/google/elephant-goldfish-model) (Apache 2.0): the Core Mandates section and the persona layout are theirs; the roles, instructions and rules are new. The Art Director and Cold Viewer prompts are new.

Written by Ashwin Ganesh Krishnamurthy.
