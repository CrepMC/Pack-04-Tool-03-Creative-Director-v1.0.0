# 01 — Scope and Boundaries

## Tool trả lời câu hỏi gì?

**“Video này nên truyền tải cảm giác, mục tiêu bán hàng và cách định vị sản phẩm như thế nào?”**

Không trả lời:
- camera quay thế nào;
- người mẫu đi ra sao;
- background bố trí gì;
- lighting cụ thể;
- lens/DOF;
- prompt generation cuối.

## Input bắt buộc

- ProductDNA LOCKED hoặc APPROVED.
- ConsistencyLockSpec.
- Optional user commercial intent.
- Optional platform intent: TikTok/Reels/catalog/landing-page ad.
- Optional campaign constraints.

## Output

`CreativeBrief` có:
- creative objective;
- concept;
- brand tone;
- audience intent;
- product emphasis hierarchy;
- message hierarchy;
- creative pacing intent;
- fashion/commercial balance;
- continuity principles;
- forbidden creative mutations;
- downstream notes.

## Boundary firewall

Nếu user/AI concept yêu cầu:
- thêm blazer;
- đổi màu áo;
- đổi cổ áo;
- bỏ mũ thật;
- thêm túi không có;
- biến quần rộng thành skinny;

Tool phải reject hoặc rewrite concept để bảo toàn ProductDNA.
