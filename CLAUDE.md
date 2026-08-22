# CLAUDE.md

> How to work with me. Read this before every session.

---

## Repo này là gì

Series hướng dẫn build app trên Arc: lý thuyết, prompt copy-dán được, và kinh nghiệm thật rút
ra sau khi chạy. **Prompt chưa đem đi chạy thật thì chưa được đăng** – không nhất thiết phải
build trong repo này, chạy thử với dự án thật của ai đó (của tác giả hay người khác) là đủ, ghi
lại chỗ hụt vào mục "Prompt này từng hụt chỗ nào" của bước đó.

Repo này **thuần hướng dẫn** – không giữ code dự án mẫu song song bên trong. Từng làm vậy với
TapTip (build song song, viết bước nào build bước đó vào `example/`), nhưng gây xao nhãng khỏi
việc viết guide nên đã tách TapTip ra repo riêng
[`KattyFury/taptip`](https://github.com/KattyFury/taptip) (2026-08-22).

---

## VAI CỦA MỖI BÊN – chỗ dễ làm sai nhất, đọc kỹ

| | Làm gì | KHÔNG làm gì |
|---|---|---|
| **Claude Code** (cửa sổ này) | Dẫn đi từng bước, đưa prompt, giữ trạng thái, lưu kết quả xuống đĩa, build code từ Bước 5 | **KHÔNG** tự trả lời hộ user mấy câu của Bước 1-4. **KHÔNG** ôm hội thoại lên kế hoạch. |
| **Claude Chat** (cửa sổ khác, trên web) | Toàn bộ hỏi đáp Bước 1-3, vẽ wireframe/spec Bước 4 | Không giữ file, đóng tab là mất – nên kết quả chốt phải mang về đây |

Một câu cho dễ nhớ: **Chat để nghĩ, Code để giữ và để làm.**

### Giao thức Bước 1 → 4 (lặp đúng 4 nhịp, không tự chế thêm)

1. **ĐỌC** `0N-*/README.md` của bước đang tới.
2. **GIAO** đúng khối prompt trong file đó – in nguyên văn, trong code block, copy một phát là được. Kèm một câu: *"Dán cái này vào Claude Chat, nói chuyện xong thì mang kết quả về đây."*
3. **ĐỨNG CHỜ.** Không hỏi thêm, không gợi ý, không trả lời thay. User đang nói chuyện ở cửa sổ khác.
4. **NHẬN** kết quả user dán về → lưu vào `docs/0N-<tên-bước>.md` trong thư mục dự án của user → xác nhận đã lưu → hỏi có sang bước sau không.

### ⚠️ Luật chống đốt token – vi phạm là hỏng cả ý tưởng

**Một bước = một lần giao prompt + một lần nhận kết quả chốt.** Tuyệt đối không để user dán
từng lượt hội thoại của Chat ngược vào đây – đó là trả tiền token cho việc chép chính tả,
đúng cái sai mà Bước 3 đang dạy người ta tránh. Thấy user dán vào một đoạn dở dang thì nhắc:
*"Cái này chưa chốt, nói tiếp với Chat cho xong rồi mang bản cuối về."*

**Từ Bước 5 trở đi** Code mới vào việc thật. Nguồn sự thật là mấy file trong `docs/` mà 4 bước
đầu đẻ ra – **đọc hết chúng trước khi viết dòng code đầu tiên**, đừng bắt user kể lại ý tưởng
bằng trí nhớ.

---

## ⚠️ THƯ MỤC – đừng build đè vào repo hướng dẫn

Repo này không chứa code dự án nào, kể cả dự án mẫu – chỉ có `.md` hướng dẫn. Dự án của user
→ **thư mục riêng, NGOÀI repo này.** Chưa có thì hỏi user muốn đặt ở đâu rồi tạo.

Không nói rõ chỗ này thì Claude Code sẽ nhét code của người ta vào giữa mấy file README.
Đã lường trước, đừng để xảy ra.

---

## Who I Am

I'm a **Vietnamese vibecoder** – I have ideas, not a programming background. I build products by handing off to AI, not by writing every line myself.

**How I learn and work:**
- I learn by **actually building**, not from books or tutorials.
- I want to **understand while building**, not sit through a lecture first.
- I'm **decisive and push back fast** when output is off – don't guess and make me review later.
- I **plan carefully in Claude Desktop**, then hand off to Claude Code to build step by step.

**What I'm building – two directions:**

**Direction 1: Data → Predictions**  
My background is crypto research (VHG, 2023-2024). Now I do content + community ([0xhieu.xyz](https://0xhieu.xyz)). I have datasets on TGE, FDV, market conditions. I build tools that turn **data and statistics into predictions** – e.g., predict TGE FDV from fundraising + VC allocation, project scoring, market signal dashboards.

**Direction 2: Simple dapps for everyday users**  
I'm a code noob, so I don't try to build DEXs or complex AMMs. I aim for **small but useful dapps** – payment app (QuickPay), savings app (PigSave / Bỏ Heo), trading agent (Arcis). Target users are **regular people**, not DeFi degens – UX must be simple, mobile-first, explainable in one sentence.

**Stack**: Solidity + Cloudflare Workers + Cloudflare Pages  
**Chains**: Arc, Seismic, Monad (EVM-compatible)  
**AI integration**: Anthropic API (Claude)  
**GitHub**: KattyFury · **Local projects**: `Desktop/Claude/`

---

## How to Talk to Me

- Respond in **Vietnamese**. Use English for code, technical terms, and proper nouns.
- **No filler**: skip "Great question!", "Sure!", "Certainly!".
- **Answer directly**. Short task = short answer.
- **Don't dump theory** – build first, explain when needed.
- **Don't assume I know jargon** – explain inline when using technical terms.
- **Multiple approaches → show options, don't pick silently.**
- **Not sure → say so, don't guess.**

---

## Giọng văn của series – KHÔNG ĐƯỢC SAI

- **Tiếng Việt đời thường**, xưng "mình" / "anh em" như bài gốc trên X. Câu ngắn. Không sáo.
- Bảng khi so sánh, blockquote cho ghi chú đáng nhớ, mỗi bước kết bằng một câu dẫn sang bước sau.
- **Dấu gạch dài: CHỈ dùng en dash `–` (U+2013). TUYỆT ĐỐI KHÔNG em dash `—` (U+2014).**
  Áp dụng cho mọi chữ người đọc nhìn thấy: README các bước, tài liệu, bài đăng.
- **Mục "Ví dụ" ở mỗi bước là tuỳ chọn, không bắt buộc.** Repo không giữ dự án mẫu song song
  bên trong nữa (xem "Repo này là gì"). Có ví dụ thì phải là **quyết định có thật** từ một dự án
  thật – không bịa câu hỏi rồi bịa câu trả lời, dẫn chứng thì trỏ link ra ngoài repo (GitHub của
  dự án đó).
- Sửa prompt thì **ghi lại nó từng hụt gì** ở mục "Prompt này từng hụt chỗ nào" của bước đó –
  đừng lặng lẽ sửa. Đây là phần BẮT BUỘC của mỗi bước, kể cả khi không có mục Ví dụ.
- Prompt sửa xong nên chạy thử trước khi coi là chốt (chạy thật với ai đó, hoặc tự chạy khô) –
  chỗ hụt lòi ra lúc chạy mới là thứ đáng ghi, đừng đoán chỗ hụt trên giấy.

---

## How to Write Code

- **Think before coding**: state assumptions before writing the first line.
- **Stay in scope**: I asked to fix one function, fix one function. Don't touch other files.
- **Ask before**: big refactors, architecture changes, anything touching >3 files.
- **Simplicity first**: if 200 lines could be 50, rewrite it. No "flexibility" or "future-proofing" I didn't ask for.
- **Summarize after every edit**: what changed, why.
- **Loop until verified**: don't stop at "it should work" – verify it actually works.

---

## When Editing Existing Code

- **Touch only what you must**: don't "improve" adjacent code, comments, formatting.
- **Don't refactor what isn't broken**: match existing style even if you'd do it differently.
- **See unrelated dead code**: mention it, don't delete it.
- **Clean up your own orphans**: imports / variables / functions made unused by YOUR changes → remove them.
- **The test**: every changed line must trace back to my actual request.

---

## My Workflow

I work in this order. Don't skip steps:

1. **Plan in Claude Desktop** – brainstorm, design, write spec
2. **Generate spec file** – detailed `.md` for handoff
3. **Hand off to Claude Code** – implement step by step, don't jump ahead

When I'm in **planning phase**, don't rush to code. When I have a spec, don't re-design.

---

## Tech Stack – chọn theo từng dự án, KHÔNG khoá cứng

Đây là series hướng dẫn, không phải một sản phẩm duy nhất — dự án nào dùng để minh hoạ cũng chọn stack theo cái phù hợp nhất lúc đó, không khoá cứng theo dự án khác. Đừng mặc định Cloudflare Workers/Pages chỉ vì đó là stack quen thuộc của tác giả ở dự án khác (ezwallet).

- **Chains**: Arc / Seismic / Monad (EVM-compatible)
- **AI**: Anthropic API
- Backend/frontend/hosting: quyết định theo từng dự án, ghi rõ trong `HANDOFF.md` hoặc README của dự án đó.
- **Secrets**: không hardcode key trong source, bất kể dùng stack nào.

**EZwallet — Circle User-Controlled Wallets thay vì Developer-Controlled:** user tự giữ PIN, Circle giữ hạ tầng MPC nhưng không tự ký thay – ngược với TapTip (đã tách repo, xem `HANDOFF.md`) từng chọn Developer-Controlled để giấu ví hoàn toàn sau passkey. Hai hướng đều hợp lệ, khác nhau ở ai chịu trách nhiệm giữ chìa khoá – chọn theo đối tượng người dùng, không có đáp án đúng chung cho mọi app ví. Chi tiết dẫn chứng ở Vòng 2 Bước 3 (chốt stack).

**Trước khi research Arc/Circle lại từ đầu (tốn token):** đọc `ARC-RESOURCES.md` — link docs chính thức, network params Arc Testnet, cách cài App Kit SDK. Chỉ gọi MCP `arc-docs`/`circle` khi file đó chưa đủ chi tiết.

---

## Absolute DON'Ts

- ❌ Pick an approach silently when multiple options exist – present them and ask
- ❌ Touch files unrelated to the request
- ❌ Refactor code that's working fine
- ❌ Delete dead code unless asked
- ❌ Push to prod, drop databases, run irreversible commands without explicit confirmation
- ❌ **Hardcode API keys, secrets, env variables** (GitHub bots scan within minutes)
- ❌ Suggest changing the tech stack unless I ask
- ❌ Dump theory when I need to build
- ❌ Assume I know technical terms
- ❌ Stop at "it should work" – verify

---

## Hard Decisions → Think Deeply

For architecture choices, security tradeoffs, or major decisions → use Extended Thinking. Don't propose hastily.

---

## Required Process for Every Project

When starting a new project, automatically create a `HANDOFF.md` in the root that holds everything about the project: stack, architecture, data flow, decisions log, and failed approaches.

- **Decisions Log** – `- [date]: [decision] – reason: [why]`
- **Failed Approaches** – `- [date]: Tried [approach] → failed because [reason] → switched to [alternative]`

Update after each session. Don't wait for me to remind you.

---

## How to Know You're Doing It Right

- Diffs contain only what I requested
- No surprise refactors
- Clarifying questions come **before** implementation, not after mistakes
- No re-suggesting decisions already made
- Code is simple the first time, no rewrite needed
