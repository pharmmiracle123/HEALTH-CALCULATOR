# Miracardiac — Clinical Workspace (Enhanced)

Premium, safety-first **static multi-page** clinical application. Every page is self-contained HTML with Tailwind CDN and inline JavaScript. No build step required.

## Pages

| Page | Purpose |
|------|---------|
| `index.html` | Public landing |
| `login.html` | Demo / session entry |
| `dashboard.html` | Workspace overview |
| `calculator.html` | 20+ explainable clinical calculators (BMI, BSA, IBW, infusion, dose, draw-up, dilution, titration, paediatric fluids, CrCl, eGFR, MAP, anion gap, corrected Ca, GCS, QTc, EDD, allowable blood loss, Parkland, contrast, effective dose, lesion volume, bed indicators, rates, diagnostic accuracy, RR/NNT) |
| `patient-records.html` | **Multi-department** patient records & reminders (Nursing vitals, Physicians SOAP-style notes, Pharmacy interventions, Surgery peri-op, Radiology follow-up, HIM flags) with due-reminder panel and CSV export |
| `medication.html` | **Drug follow-up / MAR-style** log (given / held / refused / missed / due / levels, high-alert flag, due list) |
| `handover.html` | **SBAR shift handover** notes |
| `customer-care.html` | Support intake |
| `admin.html` | Brand logo & campaign images (local or Firebase + Cloudinary) |
| `settings.html` | Clear local data, platform checklist |

## Shared features

- **Background animation** (ECG waveform + floating clinical symbols) on landing, calculator, patient records, medication, handover and other key pages. Respects `prefers-reduced-motion`.
- **PWA**: `public/manifest.webmanifest`, `public/sw.js`, SVG icons.
- **localStorage keys**: `mc-user`, `mc-history-v2`, `mc-patient-records-v1`, `mc-med-log-v1`, `mc-handover-v1`, `mc-support`, `mc-ads`, `mc-logo`.

## Privacy & safety

- Prefer **bed numbers / temporary codes**, not full patient identifiers.
- All clinical tools are **decision support only** — verify local policy and patient context.
- High-alert medicines on the medication page prompt for independent double-check.

## Firebase & Cloudinary

1. Copy `.env.example` values into the inline `CONFIG` objects on relevant pages (admin, login, etc.).
2. Deploy the included **`firestore.rules`** in the Firebase Console (or via Firebase CLI).
3. Replace the placeholder owner emails in `firestore.rules` and `OWNER_EMAILS` in `admin.html`.
4. Create an **unsigned** Cloudinary upload preset for admin image uploads.

### Firestore rules summary

- `brand/*` — public read, owner write  
- `patients/*` — signed-in create/read; owner or creator update/delete  
- `medLogs/*` — same pattern  
- `support/*` — anyone can create; owners read/manage  
- `calcHistory/{uid}/*` — user-scoped  
- Default deny

## Deploy

Serve the folder as a static site (Vercel, Netlify, nginx, or open `index.html` locally). HTTPS is required for full PWA install behaviour.

## TypeScript note

Browsers cannot run TypeScript inside static HTML. All executable logic is standard JavaScript inline per page, as requested for the “everything inside each HTML” architecture.
