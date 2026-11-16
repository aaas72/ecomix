# EcoMix — Concrete Mix Optimizer

A web tool that designs low-carbon concrete mixes. Choose a strength class and an objective, and EcoMix searches thousands of candidate mixes with recycled supplementary materials (fly ash, GGBS slag, silica fume) to find the cheapest or greenest mix that still meets TS EN 206 requirements.

![Next.js](https://img.shields.io/badge/Next.js_16-000000?style=flat-square&logo=nextdotjs&logoColor=white)
![React](https://img.shields.io/badge/React_19-20232A?style=flat-square&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)
![Recharts](https://img.shields.io/badge/Recharts-22B5BF?style=flat-square)

## Features

- **Constrained optimization** — finds the best mix for strength classes C25–C40 under three objectives: minimum cost, minimum carbon, or balanced
- **Standards compliance** — enforces a maximum water/binder ratio and minimum binder content, and shows a live compliance indicator
- **Benchmark comparison** — every result is compared with a conventional Portland-cement (OPC) mix, showing carbon reduction and cost savings per m³
- **Market prices** — sliders for cement and supplementary material prices so results reflect local costs
- **Charts and KPIs** — composition, carbon and cost breakdowns with Recharts
- **PDF report** — export the optimized mix as a report
- **Bilingual** — English and Turkish interface

## How the Optimizer Works

```text
Target class (C25–C40) + objective + material prices
                │
                ▼
Grid search over replacement ratios
  fly ash 0–35 % · slag 0–70 % · silica fume 0–10 % · water 145–170 kg
                │
                ▼
Required effective binder (Bolomey strength relation, k-value efficiency factors)
                │
                ▼
Constraint checks: w/b ≤ 0.46 · binder ≥ 300 kg/m³ · total replacement ≤ 75 %
                │
                ▼
Score each valid mix by cost, carbon, or a weighted balance ──▶ best mix
```

The engine lives in [`client/lib/OptimizationEngine.ts`](client/lib/OptimizationEngine.ts), with material properties (cost, embodied CO₂, density) and k-values defined as constants.

## Project Structure

```text
client/
├── app/                     # Next.js App Router entry
├── components/              # MixOptimizer, KPICard, PriceSlider, ComplianceIndicator, PDFExporter
│   └── translations.ts      # EN / TR strings
└── lib/OptimizationEngine.ts
```

## Getting Started

**Requirements:** Node.js 20+

```bash
cd client
npm install
npm run dev     # http://localhost:3000
```

## Disclaimer

EcoMix is an academic and engineering decision-support tool. Mix designs should be verified by laboratory trials before use in construction.

## Author

**Abdellah Sheikh** — [abdellahsheikh.dev](https://abdellahsheikh.dev) · [LinkedIn](https://www.linkedin.com/in/abdellahsheikh)
