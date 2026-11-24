# L&TY Trading (ACC)

## Project Overview
Business management web app for L&TY Trading: sales, purchases, invoices and
payments, suppliers and payables, price lists, expenses, payroll and payslips,
plus monthly and tax reports.

## Architecture
- The whole app is one file, `index.html` (~5,000 lines of inline HTML, CSS and JS).
  There is no build step, bundler or package manager.
- Libraries are loaded from CDNs: Supabase JS v2, Chart.js 4.4.0, jsPDF 2.5.1, Font Awesome 6.5.
- Data lives in Supabase tables, for example `invoices`, `invoice_items`,
  `invoice_payments`, `daily_sales`, `sale_items`, `daily_purchases`,
  `purchase_items`, `purchase_drafts`, `prices`, `product_aliases`, `suppliers`,
  `supplier_payables`, `expenses`, `payroll_employees`, `payroll_slips`.
- The theme is set with `data-theme` on `<html>`, using CSS custom properties defined on `:root`.

## Development Standards
- Keep the app as a single self-contained `index.html` unless asked otherwise.
- **Escape every user-supplied value** that goes into HTML with `esc()` (defined
  near line 1314), including values inside inline `onclick` handlers. A
  script-injection fix (commit 3386e11) depended on this.
- Match the existing style: compact JS, template literals for markup, CSS variables for colors.
- Never commit Supabase service-role keys. Only the public anon key belongs in the client.

## Testing
- No automated tests. Open `index.html` in a browser (or serve it with
  `npx serve .`) and exercise the affected screens.
- Check both dark and light themes, and phone width, for any UI change.

## Claude Code setup in this repo
- `/optimize`: `.claude/commands/optimize.md` (performance review).
- Skill: `.claude/skills/code-review-specialist/`.
- MCP: `.mcp.json` defines `codex-cli` (`npx -y codex-mcp-server`). It needs
  the Codex CLI and an OpenAI API key, and must be approved when a session starts.
