# CLAUDE.md

> How to work with me. Read this before every session.

---

## Repo này là gì

Series hướng dẫn build app trên Arc, **kèm luôn dự án mẫu** trong `example/`. Hai thứ được
build **song song**: viết bước nào thì đem bước đó ra dùng thật để build `example/`, prompt
hụt chỗ nào thì sửa lại bước đó. Prompt chưa đem đi dùng thật thì chưa được đăng.

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

- `example/` – dự án mẫu **của tác giả series**. Người đọc chỉ ĐỌC để tham chiếu, không sửa, không build đè.
- Dự án của user → **thư mục riêng, NGOÀI repo này.** Chưa có thì hỏi user muốn đặt ở đâu rồi tạo.

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
  Áp dụng cho mọi chữ người đọc nhìn thấy: README các bước, tài liệu, bài đăng. (Comment code
  tiếng Việt trong `example/` thì không bắt buộc.)
- **Ví dụ ở mọi bước dùng chung dự án trong `example/`**, nối tiếp nhau, không đổi sang sản phẩm
  khác giữa chừng. Chỉ nói những gì `example/` làm thật – cần dẫn chứng thì trỏ vào file thật,
  không chế số liệu. Quy định đầy đủ: `HANDOFF.md`.
- Sửa prompt thì **ghi lại nó từng hụt gì** ở mục "Prompt này từng hụt chỗ nào" của bước đó –
  đừng lặng lẽ sửa. Chỗ hụt mới là phần dạy được nhiều nhất.
- **Tách commit:** một commit cho phần build `example/`, một commit cho phần sửa hướng dẫn.
  `git log` là bằng chứng cho người đọc thấy prompt tiến hoá thế nào.

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

Đây là series hướng dẫn, không phải một sản phẩm duy nhất — mỗi dự án (kể cả `example/`) chọn stack theo cái phù hợp nhất lúc đó, kể cả fork nguyên sample app của Circle rồi đổi stack theo sample đó. Đừng mặc định Cloudflare Workers/Pages chỉ vì đó là stack quen thuộc của tác giả ở dự án khác (ezwallet).

- **Chains**: Arc / Seismic / Monad (EVM-compatible)
- **AI**: Anthropic API
- Backend/frontend/hosting: quyết định theo từng dự án, ghi rõ trong `HANDOFF.md` hoặc README của dự án đó.
- **Secrets**: không hardcode key trong source, bất kể dùng stack nào.

**`example/` (TapTip) — đã chốt 2026-08-07:** fork [`circlefin/arc-p2p-payments`](https://github.com/circlefin/arc-p2p-payments) (Next.js + Supabase + Circle Modular Wallets/Passkey), vì đã có sẵn passkey + gasless P2P đúng spec, không dựng lại từ đầu.

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
