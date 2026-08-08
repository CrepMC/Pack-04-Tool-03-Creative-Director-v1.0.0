# Pack 04 — Tool 03: Creative Director

**Version:** 1.0.0  
**Upstream:** T02 Product DNA  
**Downstream:** T04 Camera Director  
**Primary artifact:** `CreativeBrief`

## Mục tiêu

Creative Director biến `ProductDNA` đã LOCKED thành một **creative brief có cấu trúc** cho video quảng cáo thời trang. Tool này quyết định **ý tưởng tổng thể**, mood, commercial intent, audience framing, product emphasis, brand tone, pacing intent ở cấp khái niệm, message hierarchy và mức độ “fashion vs commerce”.

Tool này KHÔNG được:
- thay đổi Product DNA;
- thêm/bớt sản phẩm;
- quyết định lens;
- quyết định camera motion;
- biên đạo tay/chân;
- áp lighting/DOF/color grade chi tiết;
- generate video;
- generate/edit ảnh;
- viết final generation prompt.

## Quy tắc lõi

1. Product identity luôn cao hơn creative concept.
2. Creative brief phải **adapt to product**, không bắt product đổi để hợp concept.
3. Không merge vai trò với Camera Director, Motion Director, Environment Director, Cinematic Director.
4. Creative intent phải structured, không phải một paragraph “luxury cinematic fashion ad” mơ hồ.
5. Mỗi quyết định sáng tạo phải trace về business intent + ProductDNA, không dựa stereotype.
6. User có quyền override concept nhưng không được phá consistency locks.
7. Output phải đủ rõ để T04/T05/T06/T07 triển khai độc lập.

## Ba prompt chính

- `prompts/Prompt-01-Foundation-UI-Inbound-and-Creative-Framework.md`
- `prompts/Prompt-02-Concept-Generation-Scoring-and-Decision-System.md`
- `prompts/Prompt-03-Production-Hardening-Handoff-and-Release.md`

Chạy đúng thứ tự 1 → 2 → 3.

## Definition of Done

- nhập ProductDNA + ConsistencyLockSpec hợp lệ;
- không mutate ProductDNA;
- tạo 3–5 concept candidates có khác biệt thật;
- score concept theo fit/sellability/clarity/risk;
- cho user chọn hoặc chỉnh;
- xuất `CreativeBrief` schema-valid;
- handoff T04 chỉ chứa creative intent, không chứa camera instructions;
- mọi product identity locks vẫn nguyên vẹn;
- build/test/schema validation pass.
