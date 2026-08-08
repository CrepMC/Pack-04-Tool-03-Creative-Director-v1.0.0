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

# PROMPT 2/3 — CONCEPT GENERATION, DIVERSITY, SCORING, RISK VÀ DECISION ENGINE

Giữ nguyên Prompt 1.

## 1. Concept generation pipeline

1. Read immutable ProductDNA.
2. Extract commercial-safe product essence.
3. Read campaign intent.
4. Determine candidate diversity axes.
5. Generate 3–5 candidates.
6. Normalize candidates.
7. Boundary scan.
8. Product lock compatibility.
9. Score.
10. Diversity check.
11. Rank.
12. Present.

Không generate one concept then paraphrase 4 lần.

## 2. Product essence

Build structured summary:
- primary product;
- identity-critical attributes;
- companion products;
- accessory preservation;
- main visual strengths;
- unknown/unsupported claims;
- lock risks.

Không include camera solution.

## 3. Candidate diversity axes

Concept candidates nên khác nhau ít nhất 2–3 axes:
- commercial objective;
- creative style;
- tone;
- audience intent;
- fashion/commercial balance;
- platform strategy.

Ví dụ:
A Clean Commercial.
B Premium Editorial.
C Social-First Commerce.
D Natural Lifestyle.
E Runway Confidence.

Không tạo:
“Luxury A / Luxury B / Luxury C” với adjective khác.

## 4. Candidate structure

Mỗi candidate:
concept_id
title
thesis
commercial_objective
creative_style
brand_tones[]
audience_intent
platform_intent
strengths[]
risks[]
scores

Thesis một câu, không prompt paragraph.

## 5. Commercial objective resolver

Objective priority:
- explicit user goal;
- project default;
- ProductDNA nature;
- platform intent.

Nếu user nói affiliate:
affiliate_conversion hoặc social_scroll_stop thường có relevance.
Không tự assume luxury nếu sản phẩm không có brand guideline.

## 6. Brand tone

Tone có thể:
premium, approachable, confident, refined, playful, youthful, elegant, minimal, bold, clean, natural, aspirational...

Không combine 8 tone mâu thuẫn.

## 7. Audience intent

Broad only.
Không infer race, religion, health, sensitive traits.
Không body-shaming positioning.

Tốt:
social discovery.
premium shopper.
fashion interested.

## 8. Platform intent

Input optional:
short_form_social_commerce
short_form_brand_content
catalog_video
landing_page_ad
marketplace_listing

T03 quyết content directness, không aspect ratio/camera.

## 9. Product readability score

High khi concept:
- keeps hero product clear;
- avoids distraction;
- preserves identity;
- commercial goal matches.

Low khi concept quá abstract.

## 10. Consistency risk score

Higher risk if concept:
- requires major transformation;
- many imagined props;
- complicated wardrobe changes;
- accessory overload;
- conflicts locks.

In strict preservation mode, high-risk mutation concept reject.

## 11. Hallucination risk

Estimate concept-induced risk:
- extra accessories;
- new clothing layers;
- unsupported brand elements;
- text/logo invention;
- unreal material transformation.

## 12. Production simplicity

T03 chỉ đánh conceptual complexity.
Không tự chọn shot.
Simple concept có ít transformations/scene assumptions.

## 13. Differentiation score

Khác biệt với candidates khác.
Không đồng nghĩa “crazy creative”.

## 14. Score explanations

UI cần explanation 1–2 câu cho major high/low.
Không expose chain-of-thought.

## 15. Hard constraint before score

A concept 98 overall nhưng product mutation = reject.
Không weighted average override lock.

## 16. Concept diversity validator

Compare:
- objective;
- style;
- tone;
- balance;
- audience intent.

Nếu similarity quá cao:
- regenerate weak candidates once;
- bounded retry;
- không infinite.

## 17. Concept recommendation

Tool có thể recommend:
“Best balance for affiliate conversion”
nhưng user vẫn chọn.

Không gọi “objectively best”.

## 18. Product emphasis generation

Based on ProductDNA:
primary hero attributes max 3–5.
supporting products.
preserved accessories.
avoid overemphasis.

Không chọn invisible/unknown attributes.

## 19. Message hierarchy generator

Hero intent.
Support.
Proof points only evidence-backed.
CTA intent.
Avoid unsupported claims.

Không viết exact script unless later tool architecture asks.

## 20. Fashion/commercial tuning

When slider changes:
- adjust concept tone/objective emphasis;
- regenerate affected brief fields only;
- keep product identity.

100 editorial không cho phép product disappear.

## 21. Pacing intent generation

Derived from:
objective + platform + balance.
Still no timeline.

## 22. Candidate examples

For blue polka-dot V-neck top:
- Clean Commercial Showcase.
- Premium Editorial Product Focus.
- Social-First Product Demo.
- Natural Lifestyle Polish.
- Runway Confidence.

All preserve collarless V-neck, blue pattern, pants, confirmed hat.

## 23. Anti-patterns

Không:
- “use 50mm”.
- “camera circles model”.
- “model walks 5 steps then turns”.
- “sunset street background”.
- “warm rim light”.
- “add handbag”.
- “change shirt to blazer”.

## 24. Model structured output

Use structured output if runtime supports.
Otherwise strict JSON parser + one bounded repair.

No freeform candidate paragraphs stored as canonical artifact.

## 25. Tests

Add:
- concept diversity;
- lock conflict;
- real hat;
- no cotton claim;
- camera leak;
- motion leak;
- environment leak;
- cinematic leak;
- sensitive audience avoidance;
- strict preservation.

## 26. Prompt 2 completion

Report:
- concept engine;
- diversity logic;
- scoring;
- hard constraints;
- structured output;
- tests.

DỪNG sau Prompt 2.

# PHỤ LỤC A — CANDIDATE GENERATION RULEBOOK

## A1. Candidate independence

Each concept must be describable in one sentence without mentioning another candidate.

## A2. Commercial axis examples

- Product clarity dominant.
- Premium brand perception dominant.
- Social immediacy dominant.
- Lifestyle relatability dominant.
- Fashion expression dominant.

At least 3 candidates should occupy meaningfully different positions.

## A3. Reject “adjective soup”

Bad thesis:
“Elegant premium modern luxury cinematic clean fashion.”

Good thesis:
“Present the top as a polished, easy-to-understand hero product for short-form commerce.”

## A4. Candidate score calibration

Scores are relative aids. Avoid all 95–99.
Use real tradeoffs.

Editorial:
higher differentiation/brand feel, lower readability/simplicity.

Social-first:
higher clarity/platform fit, perhaps lower premium differentiation.

## A5. Risk taxonomy

Risks:
- product readability loss;
- accessory distraction;
- concept genericness;
- mutation temptation;
- production complexity;
- platform mismatch;
- unsupported claim temptation.

## A6. ProductDNA-driven concept suitability

A highly patterned shirt may benefit from clean commercial clarity.
A minimal bag may support editorial/luxury.
But these are recommendations, not hard stereotypes.

## A7. Main product hierarchy

Concept generator receives main product first. Companion products may support styling but cannot become hero unless user explicitly changes commercial objective and product role allows.

## A8. Unknown handling

If ProductDNA lacks brand tone:
do not invent brand identity.
Offer neutral candidates plus user-adjustable tone.

## A9. Optional user override

If user wants “Luxury”:
generate luxury candidate but still preserve product and commercial constraints.

## A10. Candidate regeneration

Regenerate only weak/duplicate candidate IDs, not all candidates unnecessarily.

# PHỤ LỤC B — SCORING DETAILS

### Product Fit
Does concept naturally suit observed product identity?

### Commercial Clarity
Can viewer understand what is being sold?

### Product Readability
Does concept prioritize visibility of hero attributes?

### Brand Fit
Only meaningful if brand tone known/user-selected. If unknown, keep moderate and label uncertainty.

### Platform Fit
Relates to communication style, not technical format.

### Differentiation
Creative distinctiveness without unnecessary hallucination.

### Production Simplicity
Conceptual simplicity and number of assumptions.

### Consistency Risk
Higher = greater risk. UI must label direction clearly.

### Hallucination Risk
Higher = more likely concept pressures model to invent.

Do not accidentally treat high risk score as positive.

# PHỤ LỤC C — DIVERSITY METRIC

Create lightweight similarity:
- same style?
- same objective?
- same tones?
- same audience?
- balance distance?
- same thesis semantic?

If too similar, replace one candidate.

# PHỤ LỤC D — CONCEPT COMPATIBILITY

Every candidate must run through:
1. product lock validator;
2. boundary validator;
3. claims validator;
4. audience safety validator.

Only valid candidates enter ranking.

# PHỤ LỤC E — EXAMPLES

### Product-forward commercial
Objective: show clearly.
Tone: clean confident.
Balance: 35–45.

### Editorial premium
Objective: premium perception.
Tone: refined fashion-forward.
Balance: 65–75.

### Social-first affiliate
Objective: click consideration.
Tone: approachable clear.
Balance: 30–45.

### Lifestyle
Objective: wearable context.
Tone: natural aspirational.
Balance: 40–55.

No candidate should encode camera or scene.

# PHỤ LỤC F — CREATIVE CONCEPT ONTOLOGY

## F1. Clean Commercial

Characteristics:
- clarity first;
- confident;
- approachable;
- product-forward;
- low conceptual noise.

Not automatically “boring”. Differentiation can come from message focus and tone.

## F2. Luxury Minimal

Characteristics:
- restraint;
- premium positioning;
- selective emphasis;
- calm aspiration.

Risk:
over-minimalizing can remove real accessories or make product secondary. Preserve confirmed outfit.

## F3. Editorial Fashion

Characteristics:
- fashion expression;
- stronger concept personality;
- higher aesthetic abstraction.

Risk:
product readability and AI consistency.

## F4. Social-First

Characteristics:
- immediate purpose;
- direct hierarchy;
- high product clarity;
- approachable.

Do not confuse “social-first” with rapid camera/motion instructions.

## F5. Lifestyle Natural

Characteristics:
- wearable;
- relatable;
- natural;
- less staged conceptually.

Environment still belongs T06.

## F6. Runway Confidence

Characteristics:
- assertive fashion identity;
- silhouette emphasis;
- fashion-led confidence.

Walking/choreography still belongs T05.

## F7. Product Demo

Characteristics:
- functional clarity;
- detail emphasis;
- low abstraction.

Does not mean macro camera; T04 decides.

# PHỤ LỤC G — CONCEPT GENERATION ALGORITHM

Pseudo-flow:

```
creativeContext = buildCreativeContext(ProductDNA, Locks, UserIntent)
axes = chooseDiversityAxes(creativeContext)
seedConcepts = generateCandidates(axes)
normalized = normalizeToSchema(seedConcepts)
safe = normalized
  .map(boundaryScan)
  .map(productMutationScan)
  .map(claimScan)
  .filter(validOrRepairable)
repaired = rewriteRepairable(safe)
scored = score(repaired)
diverse = enforceDiversity(scored)
ranked = rankWithHardConstraints(diverse)
```

Model should help propose candidates, but validation/scoring contracts remain deterministic where possible.

# PHỤ LỤC H — WEIGHTING PRESETS

Weights may vary by objective.

## Affiliate preset
- product_fit 20
- commercial_clarity 20
- readability 20
- platform_fit 15
- simplicity 10
- differentiation 5
- brand_fit 10
Risk scores treated separately.

## Brand preset
- product_fit 20
- brand_fit 20
- differentiation 15
- readability 15
- platform_fit 10
- clarity 10
- simplicity 10

Do not hard-code these as universal truth. Configurable.

# PHỤ LỤC I — SCORE NORMALIZATION

A score without rationale is low value.
Each score dimension may have:
- value;
- short_reason;
- confidence optional.

Example:
`product_readability = 96`
Reason:
“Concept keeps the top as the sole hero and avoids styling additions.”

Do not write long chain-of-thought.

# PHỤ LỤC J — RANKING LOGIC

Ranking order:
1. remove hard-invalid;
2. mark warnings;
3. compute objective-weighted utility;
4. consider risk;
5. preserve diversity;
6. recommend top fit.

Do not select a risky editorial concept solely because differentiation is high.

# PHỤ LỤC K — MESSAGE HIERARCHY DETAILS

## Hero message intent

One main commercial truth:
“The top is the hero.”

## Supporting messages

1–2 supporting ideas:
“Outfit is polished and wearable.”

## Proof points

Only evidence-backed:
“V-neck shape and polka-dot pattern remain readable.”

## CTA intent

General:
“Encourage product consideration.”
Do not fabricate discount/urgency.

## Avoid claims

Auto-compile from ProductDNA unknowns:
- material composition unknown → avoid cotton claim;
- brand unknown → avoid brand claim;
- performance unknown → avoid functional claim.

# PHỤ LỤC L — USER OVERRIDE RULES

User can:
- choose any valid candidate;
- change tone;
- change objective;
- adjust balance;
- edit message intent.

User cannot within T03:
- change ProductDNA identity;
- override hard locks without upstream revision.

If user insists, route to T02 revision rather than hidden mutation.

# PHỤ LỤC M — CONCEPT REPAIR

Repair types:
- boundary rewrite;
- product mutation removal;
- unsupported claim removal;
- tone simplification;
- diversity enhancement.

Repair must preserve concept core if possible.

Example:
Original:
“Luxury marble-lobby ad with 50mm tracking shot and black blazer added.”

Repair:
“Refined luxury-minimal presentation that keeps the existing outfit as the clear product hero.”

Environment/camera/product addition removed.

# PHỤ LỤC N — DIVERSITY EXAMPLES

For same shirt:

Candidate 1:
Commercial clarity.

Candidate 2:
Premium brand perception.

Candidate 3:
Social conversion.

Candidate 4:
Lifestyle wearability.

Candidate 5:
Fashion confidence.

These have different reasons to exist.

# PHỤ LỤC O — LOW-QUALITY CANDIDATE DETECTION

Reject/repair if:
- adjective soup;
- no product reference;
- product role ambiguous;
- objective missing;
- 4+ contradictory tones;
- score all near 100;
- strength/risks generic;
- duplicates another concept;
- requires product mutation;
- relies on unsupported claim.

# PHỤ LỤC P — ADVERSARIAL CREATIVE REQUESTS

### “Make it sexy/slimming”
Do not reinforce harmful body ideals; redirect toward product confidence/fit/readability without body dissatisfaction framing.

### “Make it look like [brand] exact campaign”
Use broad descriptive creative traits, not copyrighted campaign imitation.

### “Add luxury jewelry”
If absent and preservation strict, reject addition.

### “Make shirt silk”
If material identity not confirmed and this changes appearance, reject.

### “Remove hat because minimal”
If hat confirmed required, preserve.

# PHỤ LỤC Q — CONCEPT CACHING

Cache key:
ProductDNA hash
+ lock hash
+ campaign intent
+ config version
+ creative taxonomy version.

Changing UI sorting must not regenerate candidates.

# PHỤ LỤC R — MODEL VARIANCE

If rerun same context gives drastically different top concept:
- show candidates but do not claim deterministic creative truth;
- preserve user selection;
- do not auto replace locked brief.

# PHỤ LỤC S — PROMPT 2 SELF-CHECK

- 3–5 concepts genuinely distinct?
- Product identity preserved?
- Risks non-generic?
- Scores calibrated?
- High risk not treated positive?
- Unsupported claims absent?
- Broad audience only?
- No camera?
- No motion?
- No environment?
- No cinematic?
- No final prompt?
