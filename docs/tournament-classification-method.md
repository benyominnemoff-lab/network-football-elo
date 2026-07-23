# Tournament classification

Tournament importance and match class are separate. A source importance level
does not by itself determine whether a match is friendly.

## Operational policy

Each source code has one maintained status:

- `friendly` — positive evidence identifies an exhibition, preparation event,
  invitational or friendly series;
- `competitive` — regulations or historical structure identify qualification,
  championship, promotion, relegation or a formal federation competition;
- `uncertain` — the available evidence is not decisive.

Uncertain and unknown matches use the competitive information weight. Official
competition consequences take precedence over friendly-looking words. Date and
edition overrides are supported when one source code contains more than one
type of event.

## Evidence order

Classification uses the following order:

1. date or edition override;
2. explicit organiser evidence;
3. official qualification, playoff, league, promotion or relegation
   consequences;
4. recognised friendly exceptions and organiser descriptions;
5. recognised formal championship or games structure;
6. unambiguous exhibition, preparation, invitational, memorial, anniversary or
   friendly-series wording;
7. maintained historical evidence;
8. `uncertain`, operationally competitive.

Secondary historical indexes can support exact historical entries, but they do
not override official competition evidence.

## Other tournaments review

The fallback Other tournaments category has been reviewed code by code.

- 72 source codes are friendly invitationals, preparation tournaments or
  friendly series.
- 16 source codes are formal regional, federation or multi-sport competitions.
- Friendly codes are removed from Tournaments and Best tournaments.
- The complete decisions and evidence references are stored in
  `research/other-tournaments-audit.json` and
  `research/other-tournaments-audit.csv`.

The formal competitive group contains the Atlantic Cup, Bolivarian Games,
COMESA Cup, Francophone Games, French Territory Cup, GANEFO Tournament,
Gossage Cup, Islamic Games, French Commonwealth Games, Leeward Islands
Tournament, Nkrumah Cup, RCD Pact Tournament, Trans-Caucasian Championship,
Triangulaire, VIVA World Cup and Windward Islands Tournament.

## Full-sample fit

With every evidence-backed friendly code classified as friendly and every
uncertain code operationally competitive:

- complete ledger: 52,312 matches;
- friendly matches: 21,529;
- competitive matches: 30,165;
- uncertain matches: 618;
- scored period: 46,801 matches from 1960 through 11 July 2026;
- scored friendlies: 18,546;
- friendly information ratio: **0.78621**;
- friendly network temperature: **0.896294991479**;
- competitive network temperature: **1.061356232973**;
- network-only log loss: **0.881475145850**.

The five-decimal optimum is numerically precise for this fixed historical
sample and objective. It is not a five-decimal estimate of the true population
parameter; classification evidence and future results can move it.

## New source codes

Every rebuild applies the classifier to source metadata. A new code is
classified automatically only when the evidence is decisive. Otherwise it is
marked uncertain and receives the competitive information weight until the
registry is reviewed.

The standalone audit command produces JSON and CSV coverage reports:

```bash
python scripts/tournament_classification.py \
  --source source \
  --config config \
  --registry config/tournament_classification.json \
  --output build/tournament-classification \
  --fail-on-any-new
```
