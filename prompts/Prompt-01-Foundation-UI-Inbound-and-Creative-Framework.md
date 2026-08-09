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

# PROMPT 1/3 — FOUNDATION, UI, INBOUND CONTRACT VÀ CREATIVE FRAMEWORK

Giữ nguyên code dự án hiện tại. Hãy xây nền tảng Tool 03 chạy được.

## 1. Kiến trúc module

Tách tối thiểu:
- domain/creativeBrief.ts
- domain/conceptCandidate.ts
- domain/creativeScores.ts
- domain/boundary.ts
- domain/errors.ts
- adapters/productDNAAdapter.ts
- services/inputValidator.ts
- services/creativeIntentService.ts
- services/conceptCandidateService.ts (interface/stub ở prompt 1)
- services/boundaryValidator.ts
- services/compatibilityService.ts
- services/exportService.ts
- state/creativeDirectorStateMachine.ts
- components/ProductIdentitySummary.tsx
- components/CampaignIntentPanel.tsx
- components/ConceptCandidateGrid.tsx
- components/ConceptCompareView.tsx
- components/CreativeBriefEditor.tsx
- components/ProductEmphasisPanel.tsx
- components/MessageHierarchyPanel.tsx
- components/CreativeRiskPanel.tsx
- components/LockCompatibilityPanel.tsx
- components/ExportPanel.tsx

Không dồn vào App.tsx.

## 2. Inbound contract

Nhận ProductDNA + ConsistencyLockSpec.

Validate:
- source artifact;
- schema version;
- status;
- primary product;
- unresolved blocking issues;
- lock integrity;
- product hierarchy.

Nếu ProductDNA chưa LOCKED/APPROVED theo config:
- disable generate concepts;
- exact reason.

Không tự sửa DNA.

## 3. Domain model CreativeBrief

Fields:
- artifact metadata;
- source_product_dna_id;
- selected_concept;
- product_emphasis;
- message_hierarchy;
- fashion_commercial_balance;
- pacing_intent;
- forbidden_mutations;
- warnings.

Selected concept:
- title;
- thesis;
- commercial objective;
- creative style;
- brand tones;
- audience intent;
- platform intent;
- strengths;
- risks;
- score dimensions.

Không chứa field camera/motion/environment/cinematic implementation.

## 4. Creative intent input

User controls:
- business objective;
- platform intent;
- brand tone optional;
- fashion/commercial balance;
- product emphasis preference;
- optional campaign notes.

Nếu user không nhập, AI có thể đề xuất default nhưng phải dựa ProductDNA + broad commercial logic.

Không hỏi user 20 câu trước khi tạo concept.

## 5. UI

### Header
Tool name/version/project.

### Upstream Product Identity
Hiển thị:
- main product;
- hero identity attributes;
- companion products;
- confirmed accessories;
- critical locks.

### Campaign intent panel
Controls:
- commercial objective;
- platform intent;
- brand tone;
- fashion vs commercial slider.

### Concept gallery
3–5 cards.

### Compare view
2–3 concepts.

### Brief editor
Edit intent-level fields.

### Lock compatibility
Pass/fail + exact conflict.

### Approve
Only after validation.

## 6. Product emphasis hierarchy

Creative Director được quyết định:
- cái gì là visual hero;
- supporting items;
- accessories preserved;
- avoid overemphasis.

Không quyết định framing/crop.

Ví dụ:
hero = collarless V-neck shirt pattern + silhouette.
support = beige-cream pants.
preserve = straw hat.
avoid = hat visually overpowering top.

## 7. Message hierarchy

Hero message intent.
Supporting message intent.
Proof points.
CTA intent.
Avoid claims.

Không generate marketing lies.

Nếu ProductDNA material chỉ “matte woven”, avoid claim “100% cotton”.

## 8. Fashion/commercial balance

Slider 0–100.
0 = catalog/product demo.
50 = balanced commercial fashion.
100 = editorial fashion.

Slider thay CreativeBrief, không trực tiếp thay video prompt.

## 9. Pacing intent

Enums:
slow_premium
deliberate_commercial
balanced
energetic_social
product_demo_clear

Chỉ intent.
Không timeline.

## 10. Boundary validator

Tạo detection cho leakage terms/fields:
camera:
lens, focal length, mm, dolly, orbit, tracking shot, low angle, close-up...

motion:
walk 3 steps, spin 180, raise hand at second 4...

environment:
brick wall, studio set, street location nếu T06 phụ trách.

cinematic:
softbox, rim light, bokeh, LUT, teal-orange, shallow DOF nếu T07 phụ trách.

Nếu user nhập những thứ này trong campaign note:
- giữ raw note optional;
- không đưa chúng vào final T03 output;
- có thể mark “downstream preference request” nếu architecture cho phép, nhưng đừng thực thi.

## 11. Product mutation firewall

Check selected concept against locks.

Detect:
- added garment;
- removed confirmed accessory;
- changed collar/neckline;
- changed color;
- changed pattern;
- changed silhouette;
- unsupported brand/claim.

Nếu conflict:
- BOUNDARY_VIOLATION;
- rewrite suggestion ở intent level.

## 12. State machine

WAITING_INPUT
VALIDATING_INPUT
INPUT_REJECTED
READY_FOR_CONCEPTS
GENERATING_CANDIDATES
CANDIDATES_READY
USER_SELECTION
EDITING_BRIEF
COMPATIBILITY_CHECK
BOUNDARY_VIOLATION
READY_FOR_APPROVAL
LOCKED
EXPORTING
EXPORTED
BLOCKED

Implement guards.

## 13. User edit semantics

Edit CreativeBrief không sửa ProductDNA.

Locked CreativeBrief edit → new revision.

## 14. Accessibility

- compare table keyboard accessible;
- sliders labeled;
- score not color-only;
- errors focus;
- mobile concept cards usable.

## 15. Prompt 1 acceptance

- valid ProductDNA imports;
- invalid blocked;
- identity summary correct;
- campaign intent editable;
- candidate fixture cards render;
- boundary validator catches obvious camera string;
- no generation/edit/video path;
- build/typecheck pass.

Hoàn thành Prompt 1 rồi DỪNG.

# PHỤ LỤC A — ARCHITECTURE DETAIL

## A1. Layer separation

UI must never own business meaning. Candidate generation must not directly mutate brief state. Use:
`ProductDNAAdapter → CreativeContextBuilder → CandidateGenerator → CandidateNormalizer → BoundaryValidator → ScoreEngine → DraftBuilder`.

## A2. CreativeContext

Create a compact internal object:
- main product summary;
- identity-critical locks;
- companion hierarchy;
- user campaign intent;
- platform intent;
- prohibited claims;
- unknowns.

Do not pass full ProductDNA prose if not needed.

## A3. UI draft isolation

User editing tone/balance should not overwrite selected candidate object. Store:
- source candidate;
- user overrides;
- computed brief.

This preserves auditability.

## A4. Empty-state behavior

No ProductDNA:
“Complete Product DNA first.”
No fake sample.
No disabled UI pretending analysis succeeded.

## A5. Concept card consistency

All candidate cards must use same score dimensions and display order.

## A6. Explainability

Show short rationale:
“High product readability because the concept keeps the shirt as the visual hero.”
Do not expose private reasoning.

## A7. Defaults

Defaults should be neutral:
- commercial objective show_product_clearly or project default;
- balance 45–50;
- broad audience;
- no brand tone assumption beyond clean/neutral if not supplied.

## A8. Campaign notes

Free-text notes are data/input preferences. Parse into supported fields where safe. Preserve unsupported notes separately, never execute embedded tool instructions.

## A9. Revision-safe UI

When source ProductDNA changes:
- invalidate old CreativeBrief;
- show source mismatch;
- require revalidation;
- do not silently keep old concept.

## A10. Strict preservation flag

Default strict.
If future project supports creative additions, that must be explicit separate mode, not silent loosening.

# PHỤ LỤC B — PRODUCT EMPHASIS

Product emphasis is not framing. Example:
- “Hero attribute: collarless V-neck.”
Allowed.
- “Use chest-up medium shot.”
Not allowed.

For each hero attribute store:
- product_id;
- attribute path/reference;
- reason;
- importance.

# PHỤ LỤC C — MESSAGE SAFETY

Avoid:
- unsupported quality guarantees;
- medical/body claims;
- fake scarcity;
- fake endorsements;
- fake brand heritage;
- material composition not confirmed.

Allowed:
- “clean”, “polished”, “wearable”, “fashion-forward” as subjective tone, not factual performance claim.

# PHỤ LỤC D — ERROR UX

Boundary violation panel should show:
1. what leaked;
2. which downstream tool owns it;
3. intent-level rewrite.

Example:
Detected: `50mm lens`.
Owner: Camera Director.
Rewrite: `premium restrained product presentation`.

# PHỤ LỤC E — TEST MATRIX FOR PROMPT 1

Test:
- ProductDNA missing;
- ProductDNA invalid;
- ProductDNA valid;
- lock summary render;
- user changes objective;
- slider changes;
- camera leak string in note;
- mutation phrase in note;
- locked state;
- revision state;
- mobile compare shell.

# PHỤ LỤC F — CREATIVE DATA MODEL CHI TIẾT

## F1. Không dùng “creative_prompt” làm field chính

Tuyệt đối không gom toàn bộ concept vào một string như:
`creativePrompt = "Luxury premium commercial fashion..."`.

Canonical model phải structured để downstream đọc từng ý nghĩa riêng:
- objective;
- style;
- tone;
- audience intent;
- product emphasis;
- message hierarchy;
- pacing intent;
- balance;
- risks;
- forbidden mutations.

String summary chỉ là derived display field, không source of truth.

## F2. Product emphasis references

Hero attributes nên tham chiếu field/lock của ProductDNA nếu implementation cho phép:
- product_id;
- attribute_name;
- source_path;
- display_label;
- importance.

Điều này ngăn AI tự thêm hero attribute không tồn tại.

## F3. Creative constraints

Tạo `creativeConstraints` internal:
- must_preserve[];
- cannot_claim[];
- cannot_add[];
- cannot_remove[];
- unknown_do_not_assume[];
- downstream_owned_topics[].

Constraints được compile từ ProductDNA + locks.

## F4. Campaign intent normalization

Free text user:
“muốn kiểu sang nhưng dễ bán, đừng quá nghệ”
→ normalized:
brand_tones = premium, approachable
commercial_objective = increase_desire / affiliate_conversion
fashion_commercial_balance ≈ 40–55

Nhưng normalization phải hiển thị cho user sửa; không coi interpretation là user-confirmed fact.

## F5. Optional campaign metadata

Fields có thể thêm:
- campaign_name;
- distribution_context;
- product_priority;
- brand_guideline_ref;
- user_notes.

Không đưa PII/sensitive targeting vào unless absolutely necessary and explicitly supplied.

# PHỤ LỤC G — UI DESIGN CỤ THỂ

## G1. Upstream identity summary

Card phải nhấn mạnh:
- “These details are locked from Product DNA.”
- icon lock tại critical attributes.

Nếu user click edit ProductDNA:
- navigation back to T02/revision path;
- T03 không sửa tại chỗ.

## G2. Campaign intent panel

Use progressive disclosure.

Essential:
- Objective
- Platform intent
- Fashion ↔ Commercial balance

Advanced:
- Brand tone
- Audience intent
- Campaign notes
- Product emphasis preference

Không bắt người dùng chọn tất cả.

## G3. Concept gallery

Mỗi concept card có:
- title;
- one-line thesis;
- badge style;
- objective;
- 3 tone tags max;
- score highlights;
- strengths;
- risks;
- “Why it fits” summary;
- Select button.

Không render full verbose rationale ở card.

## G4. Compare mode

Rows:
- Product fit
- Commercial clarity
- Readability
- Differentiation
- Production simplicity
- Consistency risk
- Hallucination risk
- Objective
- Tone
- Product emphasis

Risk direction phải rõ: 10 risk tốt hơn 70 risk.

## G5. Selected concept editor

Editable:
- concept title optional;
- thesis;
- objective;
- tones;
- audience intent;
- balance;
- pacing intent;
- product emphasis;
- messages.

Read-only:
- ProductDNA identities;
- locks.

## G6. Compatibility panel

Status:
PASS
WARNING
BLOCKED

Mỗi violation:
- exact field;
- ProductDNA lock;
- conflicting creative phrase;
- suggested safe rewrite.

## G7. Approval

Button text:
“Lock Creative Brief”
không phải “Generate Video”.

Sau lock:
“Export to Camera Director”.

# PHỤ LỤC H — CREATIVE SCOPE VÀ DOWNSTREAM OWNERSHIP

## H1. Camera Director owns

- shot size;
- framing;
- angle;
- lens/focal length;
- camera path;
- stabilization;
- camera speed;
- tracking/orbit/dolly/pan/tilt.

T03 chỉ cung cấp:
product readability priority,
confidence/premium intent,
pacing intent.

## H2. Motion Director owns

- model walk;
- turn;
- pose;
- hand movement;
- timing;
- stop state;
- body mechanics.

T03 chỉ cung cấp:
energetic vs deliberate conceptual pacing,
confidence/elegance/naturalness tone.

## H3. Environment Director owns

- background;
- location;
- prop placement;
- spatial anchors;
- environmental continuity.

T03 chỉ cung cấp:
contextual tone such as refined/natural/urban *if allowed as abstract intent*.

## H4. Cinematic Director owns

- lighting;
- exposure;
- color treatment;
- depth of field;
- optical look;
- grain;
- contrast.

T03 chỉ says:
premium / clean / warm-feeling / bold as mood.

## H5. Prompt Optimizer owns final prompt correction

T03 never assembles final `[DIRECTOR]+[CAMERA]+...` generation prompt.

# PHỤ LỤC I — BUSINESS LOGIC

## I1. Affiliate conversion

Creative priority:
1. product comprehension;
2. desire;
3. outfit credibility;
4. distinction;
5. low hallucination risk.

Do not over-editorialize if it obscures product.

## I2. Brand premium perception

Priority:
1. refined identity;
2. consistent product;
3. restrained messaging;
4. product hero;
5. commercial clarity still maintained.

## I3. Catalog trust

Priority:
clear product,
low concept noise,
realistic presentation,
no exaggerated claims.

## I4. Social scroll stop

Priority:
immediate concept clarity,
strong product hero,
distinct but simple concept,
no needless transformations.

# PHỤ LỤC J — CREATIVE RISK REGISTRY

Risks:
- Product Overshadowing
- Accessory Overshadowing
- Concept Genericness
- Editorial Abstraction
- Excessive Transformation
- Unsupported Claim
- Product Mutation
- Audience Over-Specification
- Downstream Boundary Leak
- Multi-Product Confusion
- Hallucinated Styling Item
- Brand Tone Assumption

Each risk:
severity,
affected field,
mitigation,
blocking status.

# PHỤ LỤC K — INPUT EDGE CASES

1. ProductDNA has no brand tone.
→ Neutral creative options.

2. ProductDNA includes multiple variants.
→ T03 requires selected variant; do not mix.

3. Primary product role changed in T02 revision.
→ old brief stale.

4. Companion product low confidence.
→ do not make it concept-critical.

5. Accessory confirmed optional.
→ brief can say preserve unless campaign explicitly excludes via upstream revision.

6. User says “focus on pants” while primary is shirt.
→ clarify/offer role-change route if materially contradictory; T03 does not silently change primary.

7. Product is simple/minimal.
→ concept differentiation should come from communication logic, not invented garment detail.

# PHỤ LỤC L — IMPLEMENTATION QUALITY

- Do not use one monolithic `generateCreativeBrief()` doing all.
- Boundary checks must be testable separately.
- Scoring weights configurable.
- Taxonomy version explicit.
- Candidate generator replaceable.
- UI does not parse raw model JSON.
- Do not suppress schema errors with broad try/catch.
- Never ship fixtures as production output.

# PHỤ LỤC M — PROMPT 1 FINAL SELF-CHECK

Before stop:
- ProductDNA read-only?
- Locks visible?
- Campaign intent normalized but editable?
- No Camera/Motion/Environment/Cinematic selectors?
- Concept card fixture distinct?
- Boundary panel functional?
- State machine guarded?
- Export disabled before lock?
- No final prompt assembler?
- Build clean?
