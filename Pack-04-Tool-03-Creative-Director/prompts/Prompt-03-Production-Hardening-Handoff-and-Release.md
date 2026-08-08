# VAI TRÒ TUYỆT ĐỐI

Bạn đang xây **Tool 03 — Creative Director** trong một pipeline AI video nhiều tool độc lập.

T02 Product DNA đã xác định sản phẩm là gì.
T03 Creative Director chỉ quyết định **ý tưởng quảng cáo tổng thể**.
T04 Camera Director mới quyết định camera.
T05 Motion Director mới quyết định chuyển động.
T06 Environment Director mới quyết định môi trường.
T07 Cinematic Director mới quyết định lighting/lens look/DOF/color.
T08 QA kiểm tra.
T09 Prompt Optimizer sửa prompt.

Không được phá separation of concerns.

# PRODUCT PRESERVATION FIRST

ProductDNA và ConsistencyLockSpec là immutable truth. Creative concept phải thích nghi với sản phẩm, không được biến sản phẩm thành thứ khác.

# KHÔNG ĐƯỢC LÀM

- Không image generation.
- Không image editing.
- Không video generation.
- Không camera lens/focal length.
- Không camera move.
- Không body choreography.
- Không environment set design.
- Không lighting setup.
- Không color grade.
- Không final generation prompt.
- Không thay đổi ProductDNA.
- Không thêm/bớt phụ kiện không được phép.
- Không invent commercial claims.

# PROMPT 3/3 — PRODUCTION HARDENING, VERSIONING, HANDOFF, SECURITY, QA VÀ RELEASE

Giữ nguyên Prompt 1 + Prompt 2.

## 1. Pre-approval validation

Before READY_FOR_APPROVAL:
- CreativeBrief schema valid;
- selected concept exists;
- primary product matches ProductDNA;
- hero attributes supported;
- no unsupported claims;
- no product mutation;
- no unresolved boundary violation;
- no camera/motion/environment/cinematic instructions;
- forbidden_mutations include critical locks where appropriate.

## 2. Boundary linter

Build deterministic + semantic linter.

### Camera leakage
Detect:
lens, mm, focal length, tracking shot, dolly, orbit, low/high angle, pan, tilt, close-up, full-body shot if this architecture reserves framing for T04.

### Motion leakage
Detect exact choreography/timeline:
walk 3 steps, turn 45°, hand on hip at second 6, stop for 2 seconds.

### Environment leakage
Detect set/location construction:
brick wall, marble hall, neon street...
If user upstream has environment later, T03 should not own it.

### Cinematic leakage
Detect:
DOF, bokeh, key light, rim light, LUT, film grain, color grade, exposure recipe.

When detected:
- do not simply delete meaning;
- rewrite to intent.

## 3. Creative intent rewrite examples

Camera:
“low-angle tracking” → “confident fashion-forward presentation”.

Motion:
“slow walk then pose” → “deliberate, composed pacing with a clear final product-readability state.”

Environment:
“luxury marble lobby” → “premium and refined contextual tone.”

Cinematic:
“warm rim light” → “warm premium mood.”

## 4. Product mutation linter

Compare CreativeBrief nouns/adjectives against ProductDNA + locks.

Detect:
- new garments;
- removed items;
- changed category;
- changed colors;
- changed patterns;
- changed neckline/collar;
- invented logo;
- extra jewelry;
- material transformation.

## 5. Claims validator

Claims must be:
- visually supported;
- user-confirmed;
- or broad subjective creative tone.

Reject:
“100% cotton”
“waterproof”
“slimming”
“eco-friendly”
“luxury Italian fabric”
unless source confirms.

## 6. Audience safety

No sensitive targeting inference.
No harmful body ideals.
No demeaning appearance messaging.

Creative brief focuses product/brand intent.

## 7. Revision model

LOCKED CreativeBrief immutable.
Edit creates:
- new artifact ID;
- parent artifact;
- changed paths;
- change reason;
- version increment;
- downstream invalidation flag.

If only tone changes, ProductDNA remains same.

## 8. Canonical JSON + hash

Stable ordering.
Exclude UI transient fields.
SHA-256 integrity.

## 9. T03 → T04 handoff

Send:
- CreativeBrief ref/payload;
- ProductDNA ref;
- ConsistencyLockSpec ref;
- warnings;
- integrity.

T04 gets intent:
product emphasis;
commercial objective;
pacing intent;
 platform intent;
fashion/commercial balance;
tone.

T04 decides camera independently.

## 10. Downstream mutation firewall

If T04 later proposes camera concept that hides hero product, that's T04 validation concern; T03 should expose readability priority clearly enough.

## 11. Retry policy

Retry:
- transient model errors;
- malformed structured output one repair;
- diversity failure one bounded regeneration.

Do not retry lock conflict until model happens to ignore it. Rewrite/reject deterministically.

## 12. Performance

- cache candidates by ProductDNA hash + campaign intent + taxonomy version;
- slider edit reuses candidates where possible;
- compare view no model call;
- avoid regeneration on tab change;
- cancellation safe.

## 13. Observability

Track:
- concept generation latency;
- candidate count;
- diversity failures;
- boundary violations;
- product mutation attempts;
- unsupported claim blocks;
- user-selected candidate;
- revisions;
- export failures.

No sensitive user profiling.

## 14. Accessibility final

- scores textual;
- compare columns responsive;
- selected concept obvious;
- boundary errors jumpable;
- keyboard selection;
- mobile approve safe area.

## 15. Golden fixtures

A. blue polka-dot collarless V-neck top + beige pants.
B. same with confirmed straw hat.
C. ProductDNA with material unknown.
D. strict preservation.
E. user requests luxury mutation.

Expected:
- concept varies, product identity does not.

## 16. QA release gates

Must pass:
- 0 ProductDNA mutations in golden tests;
- 0 camera/motion/environment/cinematic leakage in canonical artifact;
- 0 unsupported material claims;
- candidate diversity threshold;
- schema validation 100%;
- handoff valid.

## 17. Boundary non-goals

Do not “helpfully” implement T04–T09 here.
Do not create camera planner.
Do not create motion timeline.
Do not create environment editor.
Do not create cinematic presets.

## 18. Final scenario

Input:
blue collarless V-neck black polka-dot top, beige-cream wide-leg pants, optional confirmed straw hat.

Campaign:
affiliate conversion, social short-form, clean premium.

Expected CreativeBrief:
- Clean Commercial Fashion Showcase likely ranked high.
- Main shirt visual hero.
- pants supporting.
- hat preserved if confirmed.
- no collar mutation.
- no bag invention.
- no “100% cotton”.
- no lens/motion/light/background details.
- deliberate commercial pacing intent.
- handoff T04 valid.

## 19. Release outputs

Create/update:
README,
schemas,
tests,
changelog,
validation docs.

Run build/typecheck/tests.
Fix failures.
Do not claim “production-ready” if capability adapter is still mocked.

Kết thúc Pack 4 sau Prompt 3.

# PHỤ LỤC A — BOUNDARY LINTER IMPLEMENTATION

Use both:
- deterministic forbidden-field/keyword scan;
- semantic classifier for paraphrases.

But do not over-block ordinary words:
“focus” can mean product emphasis, not camera focus.
“dynamic” can mean tone, not camera move.

Boundary linter returns:
- violation code;
- source field;
- detected phrase;
- owner tool;
- rewrite suggestion;
- severity.

# PHỤ LỤC B — MUTATION DIFF

Build normalized product nouns/adjectives from ProductDNA.

If concept mentions unreferenced garment:
flag.

If concept says “collared shirt” while collar:none:
critical mutation.

If concept says “blue top” while blue confirmed:
compatible.

If concept says “navy” while only blue confirmed:
potential color mutation; warn/reject based strictness.

# PHỤ LỤC C — Handoff compactness

T04 gets:
- creative style;
- commercial objective;
- brand tones;
- product emphasis;
- pacing intent;
- platform intent;
- readability priority;
- risk notes.

T04 does not need concept score explanations unless debug.

# PHỤ LỤC D — Version changes

If ProductDNA source revision changes:
CreativeBrief status becomes STALE.
Do not export stale brief.

If only CreativeBrief tone changes:
invalidate T04 downstream outputs created from previous brief.

# PHỤ LỤC E — Failure recovery table

- model timeout → retry bounded;
- duplicate concepts → regenerate duplicate only;
- lock conflict → rewrite candidate, no blind retry;
- unsupported claim → remove/rewrite claim;
- boundary leak → rewrite to intent;
- schema invalid → one repair;
- unsupported runtime → block.

# PHỤ LỤC F — Golden-case assertions

For collarless V-neck fixture:
assert no string matching:
shirt collar,
lapel,
blazer,
50mm,
dolly,
orbit,
walk three steps,
rim light,
brick wall,
100% cotton.

Assert hero attribute includes neckline/pattern.
Assert pants remain supporting.
Assert confirmed hat preservation.

# PHỤ LỤC G — Release self-audit

Before completion ask:
- Did I accidentally build Camera Director?
- Did I accidentally build Motion Director?
- Did I create scene presets?
- Did I create lighting presets?
- Did I mutate ProductDNA?
- Did I overclaim ad effectiveness?
- Did I infer sensitive audience?
- Did I allow unsupported product claims?
- Did I skip schema validation?
- Did I export stale brief?

Fix before reporting complete.

# PHỤ LỤC H — PRODUCTION VALIDATION MATRIX

## H1. Schema

Every exported artifact:
- exact artifact_type;
- supported schema version;
- no unexpected top-level fields;
- selected concept complete;
- score types correct;
- balance 0–100.

## H2. Referential integrity

- source_product_dna_id resolves;
- primary product resolves;
- hero attribute refs resolve if refs used;
- preserved accessory IDs resolve;
- lock refs resolve.

## H3. Semantic integrity

No hero attribute contradicts ProductDNA.
No message proof point unsupported.
No forbidden mutation missing for critical known risk.

# PHỤ LỤC I — STALE ARTIFACT MANAGEMENT

CreativeBrief stores source hash/version.
If ProductDNA or lock hash changes:
- status STALE internally;
- disable export;
- diff upstream changes;
- rerun compatibility;
- regenerate only if necessary.

A color correction in T02 may affect concept text.
A noncritical evidence note may not require full regeneration.

# PHỤ LỤC J — DOWNSTREAM INVALIDATION

When locked brief changes:
- mark T04/T05/T06/T07 outputs based on old brief stale according orchestration layer;
- T03 itself should emit `downstream_invalidation_reason`.

Do not directly modify downstream artifacts.

# PHỤ LỤC K — SAFE SEMANTIC LINTER

Keyword-only false positives must be reduced.

Examples:
“focus on product” = creative emphasis, allowed.
“camera focus” = T04/T07 implementation, blocked.

“dynamic brand tone” = allowed.
“dynamic orbit camera” = blocked.

Use field context + semantic classifier.

# PHỤ LỤC L — CANONICAL CREATIVE SUMMARY

Optional derived summary can be generated from structured brief:

`Commercial-clean, approachable premium product showcase. The blue polka-dot collarless V-neck top remains the hero, beige-cream pants support the outfit, and confirmed accessories are preserved. Prioritize clear product readability and affiliate consideration with deliberate commercial pacing.`

This summary is display/handoff convenience, not final video prompt.

# PHỤ LỤC M — EXPORT OPTIONS

Dev/debug:
- CreativeBrief.json
- HandoffEnvelope.json
- ValidationReport.json

Production:
- in-memory artifact or platform-native storage.

Do not export raw model candidate response as canonical file.

# PHỤ LỤC N — OBSERVABILITY DEFINITIONS

`boundary_violation_rate`
= candidates with violation / candidates generated.

`mutation_attempt_rate`
= candidates conflicting with product locks / candidates generated.

`candidate_diversity_failure`
= regeneration due similarity.

`human_override_rate`
= selected/edited concept differs from recommended.

These are engineering metrics, not ad performance metrics.

# PHỤ LỤC O — NO PERFORMANCE CLAIM

Tool must never report:
“This concept will increase conversion by 35%”
unless real experiment data exists.

It may say:
“Designed for clearer affiliate conversion intent.”

# PHỤ LỤC P — RELEASE SECURITY REVIEW

Review:
- Prompt injection from ProductDNA free text;
- Output injection into T04;
- unescaped brand/logo text;
- unsafe URLs if metadata contains URLs;
- log content;
- stale artifact export.

# PHỤ LỤC Q — CONCURRENCY

If user starts concept generation twice:
- latest request ID wins;
- old response cannot overwrite current state.

If input ProductDNA changes during generation:
- cancel/ignore old response.

# PHỤ LỤC R — ERROR RECOVERY UX

Examples:

`CD_CONCEPT_MUTATES_PRODUCT`
Message:
“Concept suggests a collared version, but Product DNA locks the top as collarless.”
Action:
“Rewrite concept safely.”

`CD_BOUNDARY_CAMERA_LEAK`
Message:
“Camera implementation belongs to Camera Director.”
Action:
“Convert to creative intent.”

`CD_UNSUPPORTED_CLAIM`
Message:
“Cotton composition is not confirmed by Product DNA.”
Action:
“Remove claim.”

# PHỤ LỤC S — TEST SUITE EXTENSION

Automated or fixture tests:
1. stale ProductDNA.
2. concurrent generation.
3. duplicate concept repair.
4. candidate with high risk.
5. candidate with 50mm.
6. candidate with body choreography.
7. candidate with scene.
8. candidate with lighting.
9. candidate with unconfirmed cotton.
10. candidate removes hat.
11. candidate adds bag.
12. user changes tone.
13. user changes balance.
14. locked revision.
15. T04 handoff.
16. unsupported major version.
17. hash mismatch.
18. source product missing.

# PHỤ LỤC T — FINAL GOLDEN BRIEF EXPECTATION

For project fixture:

Primary:
blue short-sleeve top,
black polka dots,
collarless V-neck.

Supporting:
beige-cream wide-leg pants.

Accessory:
straw hat only if confirmed.

A strong commercial brief may say:
- Objective: affiliate conversion.
- Style: commercial_clean.
- Tones: clean, premium, approachable, confident.
- Product hero: neckline, blue/black pattern, upper garment silhouette.
- Supporting: pants.
- Preserved: hat.
- Pacing intent: deliberate_commercial.
- Balance: roughly 35–50.

It must NOT say:
- 50mm;
- low angle;
- dolly;
- 45-degree turn;
- one hand on hip;
- brick wall;
- warm key light;
- shallow DOF;
- add handbag;
- collared shirt;
- 100% cotton.

# PHỤ LỤC U — TOOL MAKER FINAL CHECKLIST

Before final response:
- build passed;
- tests passed;
- schemas parse;
- no stub used as real;
- no fake success;
- no product mutation;
- no unsupported claims;
- no sensitive targeting;
- no downstream implementation leak;
- locked artifact immutable;
- handoff valid;
- changelog updated.

Only then mark Tool 03 implementation complete.
