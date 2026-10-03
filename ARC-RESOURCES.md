# Tài nguyên Arc & Circle

> Tra cứu nhanh trước khi research lại từ đầu bằng MCP — đỡ tốn token. Link lấy từ MCP `arc-docs` + `circle`, verify ngày 2026-08-11, không phải đoán. Nếu nghi ngờ đã đổi, tra lại qua MCP trước khi tin file này.

## Docs chính thức

- **Arc Docs**: https://docs.arc.io — khái niệm chain, RPC, deploy contract, connect wallet, evm differences.
- **Arc App Kit** (SDK Bridge/Swap/Send/Unified Balance): https://docs.arc.io/app-kit
- **Arc Studio** (AI coding agent của Circle, ra 09/2026): https://studio.arc.io – viết, preview, deploy app/contract lên **Arc testnet** (không deploy mainnet). Chuyên tech hơn AI của docs, thử được thật. Docs: https://docs.arc.io/ai/arc-studio. CLI cho Claude Code giao việc on-chain: `npm install -g @circle-fin/arc-studio-cli` → `arc-studio login` → `arc-studio skills install --tool claude-code` (docs: https://docs.arc.io/ai/arc-studio-cli, verify 2026-10-03).
- **Circle Developer Docs**: https://developers.circle.com — Wallets (dev/user-controlled, modular), CCTP, Smart Contract Platform.
- **Circle Console** (API key, kit key, entity secret, wallet sets): https://console.circle.com

## Arc Testnet — network params

| Field | Value |
|---|---|
| Chain ID | `5042002` |
| RPC (HTTPS) | `https://rpc.testnet.arc.io` |
| RPC (WebSocket) | `wss://rpc.testnet.arc.io` |
| Block explorer | https://testnet.arcscan.app |
| Faucet | https://faucet.circle.com |
| Gas token | USDC (native, 18 decimals on-chain — hiển thị UI dùng 6 decimals kiểu ERC-20) |
| CCTP domain | `26` |

## App Kit SDK — cài đặt

```bash
npm install @circle-fin/app-kit          # full: Bridge + Swap + Send + Unified Balance
npm install @circle-fin/bridge-kit       # chỉ bridge
npm install @circle-fin/swap-kit         # chỉ swap
npm install @circle-fin/unified-balance-kit
```

Kèm đúng 1 adapter theo stack đang dùng: `@circle-fin/adapter-viem-v2`, `@circle-fin/adapter-ethers-v6`, `@circle-fin/adapter-solana-kit`, hoặc `@circle-fin/adapter-circle-wallets` (server-side, dùng chung Developer-Controlled Wallets).

## Brand assets

Chưa có bộ media kit public để tải — docs Arc ghi thẳng "contact the Arc team for logo files". Đừng tự chế logo/icon Arc; nếu cần thì hỏi user liên hệ team Arc trực tiếp.

## Cách dùng file này

Đọc file này trước khi gọi MCP `arc-docs`/`circle` research lại từ đầu. Chỉ tra MCP khi cần chi tiết sâu hơn bảng trên (code mẫu cho 1 quickstart cụ thể, API reference đầy đủ, sản phẩm Circle chưa liệt kê ở đây).
