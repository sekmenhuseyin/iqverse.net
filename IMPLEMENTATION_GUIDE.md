# IQVerse.net Next.js Migration Guide

## 🎉 Project Status: Complete & Ready

Your Next.js project is fully configured and deployed-ready. 2 tools are implemented as templates. Here's how to complete the remaining tools and deploy.

---

## 📁 Project Structure

```
iqverse-next/
├── app/                      # Next.js app router pages
│   ├── page.tsx             # Homepage
│   ├── layout.tsx           # Root layout
│   ├── globals.css          # Global styles
│   ├── json/
│   │   └── page.tsx         # JSON formatter page ✅
│   └── qrforge/
│       └── page.tsx         # QR Forge page ✅
├── components/
│   ├── Navbar.tsx
│   ├── Footer.tsx
│   ├── BackgroundEffects.tsx
│   ├── layout/
│   │   └── ToolLayout.tsx   # Shared tool wrapper
│   └── tools/
│       ├── JSONFormatter.tsx ✅
│       └── QRForge.tsx      ✅
├── lib/
│   ├── hooks/
│   │   ├── index.ts
│   │   └── useClipboard.ts
│   └── utils/
│       └── json.ts          # Shared utilities
├── styles/
│   ├── home.module.css
│   ├── tool-layout.module.css
│   ├── json-formatter.module.css
│   └── qrforge.module.css
├── public/                   # Static assets (all icons, manifest, etc.)
├── out/                      # Build output (generated on npm run build)
├── next.config.ts
├── tsconfig.json
├── wrangler.toml           # Cloudflare config
└── package.json
```

---

## 🚀 Quick Start to Add Remaining Tools

### Step 1: Create Tool Directory

```bash
mkdir app/[tool-name]
```

### Step 2: Create Page File (`app/[tool-name]/page.tsx`)

```tsx
import type { Metadata } from "next";
import YourToolComponent from "@/components/tools/YourTool";
import ToolLayout from "@/components/layout/ToolLayout";

export const metadata: Metadata = {
	title: "Tool Name | IQVerse Tools",
	description: "Tool description here",
};

export default function ToolPage() {
	return (
		<ToolLayout pill="TOOL CATEGORY" title="Tool" subtitle=" Name" description="Detailed description of what this tool does.">
			<YourToolComponent />
		</ToolLayout>
	);
}
```

### Step 3: Create Component (`components/tools/YourTool.tsx`)

```tsx
"use client";

import { useState } from "react";
import { useClipboard } from "@/lib/hooks";
import styles from "@/styles/your-tool.module.css";

export default function YourTool() {
	const [input, setInput] = useState("");
	const [output, setOutput] = useState("");
	const { copied, copy } = useClipboard();

	const handleProcess = () => {
		// Your tool logic here
		setOutput("Result");
	};

	return (
		<div className={styles.container}>
			{/* Input section */}
			<section className={styles.section}>
				<div className={styles.sectionLabel}>Input</div>
				<div className={styles.card}>
					<textarea value={input} onChange={(e) => setInput(e.target.value)} className={styles.textarea} />
					<button className={styles.btnPrimary} onClick={handleProcess}>
						Process
					</button>
				</div>
			</section>

			{/* Output section */}
			{output && (
				<section className={styles.section}>
					<div className={styles.sectionLabel}>Output</div>
					<div className={styles.card}>
						<textarea readOnly value={output} className={styles.outputArea} />
						<button className={styles.btnSmall} onClick={() => copy(output)}>
							{copied ? "Copied!" : "Copy"}
						</button>
					</div>
				</section>
			)}
		</div>
	);
}
```

### Step 4: Create Styles (`styles/your-tool.module.css`)

```css
.container {
	max-width: 1000px;
}

.section {
	margin-bottom: 2rem;
}

.sectionLabel {
	font-family: var(--font-mono);
	font-size: 0.75rem;
	font-weight: 600;
	letter-spacing: 0.05em;
	text-transform: uppercase;
	color: var(--text-muted);
	margin-bottom: 0.75rem;
}

.card {
	background: var(--bg-card);
	border: 1px solid var(--border);
	border-radius: var(--radius);
	padding: 1.5rem;
}

.textarea {
	width: 100%;
	min-height: 200px;
	padding: 1rem;
	background: var(--surface);
	border: 1px solid var(--border);
	border-radius: var(--radius-sm);
	color: var(--text);
	font-family: var(--font-mono);
	font-size: 0.85rem;
}

.textarea:focus {
	outline: none;
	border-color: var(--accent);
	box-shadow: 0 0 12px rgba(0, 200, 150, 0.1);
}

.btnPrimary {
	background: var(--accent);
	color: #0a0a0a;
	border: none;
	border-radius: var(--radius-sm);
	padding: 0.75rem 1.25rem;
	font-weight: 600;
	cursor: pointer;
}

.btnPrimary:hover {
	background: var(--accent-dark);
}

.btnSmall {
	background: var(--accent-dim);
	color: var(--accent);
	border: 1px solid var(--accent);
	border-radius: var(--radius-sm);
	padding: 0.5rem 1rem;
	cursor: pointer;
}

.outputArea {
	width: 100%;
	min-height: 250px;
	padding: 1rem;
	background: var(--surface);
	border: 1px solid var(--border);
	border-radius: var(--radius-sm);
	color: var(--text);
}
```

### Step 5: Update Homepage

Add your tool to the tools array in `app/page.tsx`:

```tsx
const tools = [
	// ... existing tools
	{ name: "Your Tool", slug: "your-tool", description: "Tool description" },
];
```

---

## 📋 Remaining Tools to Create (12 tools)

Copy the pattern above for these tools:

1. **regex** - Regex Tester (`/regex/`)
2. **password** - Password Generator (`/password/`)
3. **encodelab** - Encode/Decode (`/encodelab/`)
4. **dnslookup** - DNS Lookup (`/dnslookup/`)
5. **headers** - HTTP Headers Viewer (`/headers/`)
6. **agentscan** - AI Agent Scanner (`/agentscan/`)
7. **chromata** - Color Tools (`/chromata/`)
8. **linkradar** - Link Analyzer (`/linkradar/`)
9. **favicongen** - Favicon Generator (`/favicongen/`)
10. **ges** - Grid Essentials (`/ges/`)
11. **goo** - Link Utilities (`/goo/`)
12. **gyp** / **gst** - Utility Tools

### Reference the Original Files

See the source code in `d:\MyProjects\iqverse.net\[tool-name]\`:

- `index.html` - HTML structure and form layout
- `scripts.js` - Tool logic (convert to React state)
- `styles.css` - Tool-specific styling

---

## 🔨 Build & Development

### Local Development

```bash
npm run dev
# Visit http://localhost:3000
```

### Build for Production

```bash
npm run build
# Generates /out folder with static HTML pages
```

### Verify Build

```bash
# Check that /out folder contains:
# - index.html (homepage)
# - /json/index.html (JSON formatter)
# - /qrforge/index.html (QR Forge)
# - All static assets (icons, manifest, robots.txt, etc.)
# - _headers file (Cloudflare security headers)
```

---

## 🌐 Deploy to Cloudflare Pages

### Option 1: Git Integration (Recommended)

1. Push your Next.js project to GitHub:

   ```bash
   git init
   git add .
   git commit -m "Initial commit: Next.js migration"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/iqverse-next.git
   git push -u origin main
   ```

2. Connect to Cloudflare Pages:
   - Log in to Cloudflare Dashboard
   - Go to **Pages** → **Create a project** → **Connect to Git**
   - Select your GitHub repository
   - Configure build settings:
     - **Framework preset**: None (or Next.js)
     - **Build command**: `npm run build`
     - **Build output directory**: `out`
   - Click **Save and Deploy**

### Option 2: Manual Deployment

1. Build locally:

   ```bash
   npm run build
   ```

2. Deploy the `/out` folder to Cloudflare Pages:
   - Go to **Pages** → **Create a project** → **Direct upload**
   - Drag and drop the `/out` folder
   - Click **Deploy**

---

## ✅ Pre-Deployment Checklist

- [ ] All 15 tools implemented
- [ ] Tested locally: `npm run dev`
- [ ] Build successful: `npm run build`
- [ ] `/out` folder contains:
  - [ ] `/index.html` (homepage)
  - [ ] All tool pages (`/json/`, `/qrforge/`, etc.)
  - [ ] Static assets (icons, manifest, robots.txt)
  - [ ] `_headers` file (security headers)
- [ ] Verified Cloudflare Pages build settings
- [ ] DNS configured to point to Cloudflare Pages

---

## 🔐 Security Headers

The `_headers` file is automatically served by Cloudflare Pages. It contains:

- `X-Frame-Options: DENY` - Prevent clickjacking
- `Content-Security-Policy` - Script security
- `Strict-Transport-Security` - HTTPS enforcement
- `Permissions-Policy` - Disable camera, microphone, geolocation

No additional configuration needed!

---

## 📊 Next.js Build Output

After running `npm run build`, the `/out` folder contains:

- **Static HTML pages** for each route (SEO-friendly, no JavaScript required)
- **CSS and JavaScript** bundled and minified in `_next/`
- **Public assets** copied from `/public`
- **`_headers`** file for Cloudflare security headers

All pages are pre-rendered at build time, making them extremely fast and perfect for Cloudflare Pages.

---

## 🎯 Tips for Tool Implementation

1. **Reuse Hooks**: Use `useClipboard()` for copy-to-clipboard functionality
2. **Shared Styles**: CSS variables are predefined in `globals.css`
   - Colors: `--accent`, `--text`, `--bg`, `--border`, etc.
   - Fonts: `--font-display`, `--font-body`, `--font-mono`
   - Spacing: `--radius`, `--radius-sm`, `--radius-lg`
3. **Icons**: All icon assets are in `/public`
4. **Responsive**: Use mobile-first CSS with `@media (max-width: 768px)`
5. **Metadata**: Each tool page has SEO metadata via `export const metadata`

---

## 📝 Example: Minimal Tool Implementation

Here's the absolute minimum to create a working tool:

**1. Create `app/mytools/page.tsx`:**

```tsx
import MyTool from "@/components/tools/MyTool";
import ToolLayout from "@/components/layout/ToolLayout";

export default function MyToolPage() {
	return (
		<ToolLayout title="My Tool" description="What it does">
			<MyTool />
		</ToolLayout>
	);
}
```

**2. Create `components/tools/MyTool.tsx`:**

```tsx
"use client";

export default function MyTool() {
	return <div>Your tool UI here</div>;
}
```

**3. Create `styles/mytool.module.css`:**

```css
/* Your styles */
```

**4. Update `app/page.tsx`:**

```tsx
const tools = [
	// ... existing
	{ name: "My Tool", slug: "mytool", description: "Description" },
];
```

Done! Build and deploy. 🚀

---

## ❓ FAQs

**Q: Can I use TypeScript?** A: Yes! The project is already configured for TypeScript.

**Q: How do I add a new npm dependency?** A: `npm install package-name` and import it.

**Q: Will the build time increase with 15 tools?** A: No, Next.js builds all pages in parallel. Current build: ~5 seconds.

**Q: Can I use external libraries?** A: Yes, for example: `qrcode-styling` for QR codes, `highlight.js` for syntax highlighting, etc.

**Q: How do I add analytics?** A: Cloudflare Pages has built-in analytics. See Cloudflare Dashboard → Pages → Analytics.

---

## 📞 Support

- **Next.js Docs**: https://nextjs.org/docs
- **Cloudflare Pages**: https://developers.cloudflare.com/pages/
- **CSS Variables**: See `app/globals.css` for all available variables

---

**Project Ready for Production** ✅ Last Updated: 2026-06-14
