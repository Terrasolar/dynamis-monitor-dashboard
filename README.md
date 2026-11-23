# Dynamis Monitor — Dashboard

Static page reading `cotacoes_distribuidores` live from Supabase and rendering a price-comparison table per module/inverter/estrutura family.

Requires login (Supabase email/password). It used to read with the anon key, which is public by definition, so anyone with the URL could pull the whole supplier cost table — finding SEG-1 of the CRM audit, closed on 2026-11-23. The access token lives in sessionStorage, so it dies with the tab.

Served via GitHub Pages — https://terrasolar.github.io/dynamis-monitor-dashboard/

Source of truth / backend: the `dynamis-monitor` project (private, local).
