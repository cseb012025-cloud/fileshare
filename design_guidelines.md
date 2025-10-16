# Design Guidelines: Secure File Transfer Application

## Design Approach

**Selected Approach:** Design System - Material Design 3 (Modified)
**Justification:** This is a utility-focused file transfer tool where clarity, efficiency, and trust are paramount. Material Design 3 provides excellent patterns for file handling, progress indicators, and form interactions while maintaining a modern, professional appearance suitable for data teams.

**Key Design Principles:**
- **Clarity First:** Every action and state must be immediately understandable
- **Trust & Security:** Visual cues reinforce the application's security features
- **Efficient Workflows:** Minimize friction in upload and download processes
- **Professional Polish:** Clean, modern aesthetics that inspire confidence

---

## Core Design Elements

### A. Color Palette

**Dark Mode (Primary):**
- Background: 220 15% 8% (deep navy-charcoal)
- Surface: 220 12% 12% (elevated cards)
- Surface Variant: 220 10% 16% (input fields, secondary surfaces)
- Primary: 210 100% 58% (vibrant blue - trust and technology)
- Primary Hover: 210 100% 65%
- Success: 142 70% 50% (file upload success, active transfers)
- Warning: 38 95% 60% (expiration warnings)
- Error: 0 72% 55% (failed uploads, invalid codes)
- Text Primary: 0 0% 95%
- Text Secondary: 0 0% 65%
- Border: 220 10% 22%

**Light Mode:**
- Background: 0 0% 98%
- Surface: 0 0% 100%
- Surface Variant: 220 15% 96%
- Primary: 210 100% 48%
- Text Primary: 220 15% 15%
- Text Secondary: 220 10% 40%

### B. Typography

**Font Stack:**
- Primary: 'Inter' (Google Fonts) - all interface text
- Monospace: 'JetBrains Mono' (Google Fonts) - 6-digit codes, file sizes

**Type Scale:**
- Hero/Display: 48px (3rem), font-weight 700, line-height 1.1
- H1: 32px (2rem), font-weight 700, line-height 1.2
- H2: 24px (1.5rem), font-weight 600, line-height 1.3
- H3: 20px (1.25rem), font-weight 600, line-height 1.4
- Body Large: 16px (1rem), font-weight 400, line-height 1.6
- Body: 14px (0.875rem), font-weight 400, line-height 1.5
- Caption: 12px (0.75rem), font-weight 400, line-height 1.4
- Code/Digits: 24px (1.5rem), font-weight 500, letter-spacing 0.2em

### C. Layout System

**Spacing Scale:** Use Tailwind units of 2, 4, 6, 8, 12, 16, 24
- Component padding: p-6 to p-8
- Section gaps: gap-6 to gap-12
- Form field spacing: space-y-6
- Card spacing: p-8
- Page margins: px-4 md:px-8

**Container Strategy:**
- Max-width: 1200px (max-w-6xl)
- Upload/Retrieve forms: max-w-2xl (centered)
- File lists: max-w-4xl

### D. Component Library

**Navigation (Top Bar):**
- Height: 64px fixed
- Logo + app name left-aligned
- View toggle (Upload/Retrieve) center or right-aligned
- Dark mode toggle far right
- Border-bottom with subtle shadow

**Upload Form (Sender View):**
- Large drag-and-drop zone (min-height 320px)
- Dashed border (border-dashed) with rounded corners (rounded-2xl)
- Cloud upload icon (64px) centered when empty
- File/folder picker buttons below drop zone
- Settings card below: TTL dropdown, password input (optional toggle), max downloads input
- Primary CTA: "Generate Transfer Code" button (w-full, large size)

**Success State (After Upload):**
- Prominent 6-digit code display (monospace font, 48px, letter-spaced, in bordered card)
- QR code image (256px x 256px) centered
- Copy-to-clipboard button next to code
- Transfer details grid: expiry time, file count, total size, download limit
- Share link with copy button
- "Create Another Transfer" secondary button

**Retrieve Form (Receiver View):**
- Clean centered layout (max-w-md)
- Large 6-digit code input (6 individual digit boxes with auto-focus progression)
- Password input (appears if required)
- "Access Files" primary button
- Error states clearly displayed below input

**File List Display:**
- Table or card list with file icons (based on extension)
- Columns: filename, size, type
- Individual download buttons + "Download All as ZIP" primary action
- Download progress bar when active
- Remaining downloads counter if limit set

**Progress Indicators:**
- Linear progress bar (h-2, rounded-full)
- Percentage text below (text-sm)
- File-by-file progress for multiple uploads
- Smooth transitions (transition-all duration-300)

**Forms & Inputs:**
- Input fields: h-12, rounded-lg, border with focus ring
- Dropdowns: Custom styled select with chevron icon
- Toggles: Switch component for optional features
- Labels: text-sm font-medium, mb-2
- Help text: text-xs text-secondary, mt-1

**Cards:**
- Background: Surface color
- Padding: p-8
- Border: 1px solid border color
- Border-radius: rounded-2xl
- Subtle shadow: shadow-lg with low opacity

**Buttons:**
- Primary: h-12, px-8, rounded-lg, bg-primary, font-medium
- Secondary: outlined variant with border-2
- Icon buttons: 40px x 40px, rounded-lg
- Hover states: brightness increase + subtle scale (transform scale-105)

### E. Animations

**Minimal, Purposeful Motion:**
- File upload: Fade-in list items as they're added (duration-200)
- Code generation: Brief success pulse animation
- Progress bars: Smooth width transitions
- Button hovers: Subtle scale and brightness (duration-150)
- View transitions: Fade between Upload/Retrieve (duration-300)
- NO scroll animations or parallax effects

---

## View-Specific Guidelines

### Landing/Initial State
- Split view toggle at top: Upload | Retrieve tabs
- Active view highlighted with primary color underline
- Empty state illustration in inactive view (simple iconography)

### Upload View Deep Dive
- Hero heading: "Share Files Securely" (h1)
- Subheading: "Upload files or folders. Generate a code. Share instantly." (text-lg, text-secondary)
- Drop zone prominence: Largest visual element
- Progressive disclosure: Settings collapse/expand if multiple options
- Mobile: Stack form elements vertically, maintain touch-friendly 44px minimum tap targets

### Retrieve View Deep Dive  
- Hero heading: "Retrieve Your Files" (h1)
- Clean, distraction-free input area
- 6-digit boxes with subtle animation on focus
- Error messaging: Red text below input with icon
- Loading state: Spinner + "Accessing transfer..." text

---

## Images

**No Large Hero Image** - This utility app doesn't need hero imagery. Instead:
- Use iconography: Cloud upload, lock, download, QR code icons from Material Symbols or Heroicons
- File type icons: Document, image, video, archive icons (16px-24px)
- Empty state illustrations: Simple, outlined SVG illustrations (not photography)
- QR codes: Dynamically generated, displayed at 256px x 256px

**Icon Usage:**
- Drop zone: Cloud arrow up icon (64px, stroke-2, text-primary)
- Success: Check circle (32px, text-success)
- Security: Lock icon next to password fields
- Copy: Clipboard icon in copy buttons
- All icons from Heroicons library via CDN

---

## Responsive Behavior

**Breakpoints:**
- Mobile: < 768px - Single column, full-width forms, stacked elements
- Tablet: 768px - 1024px - Two-column layouts for settings, larger touch targets
- Desktop: > 1024px - Optimal layout with max-width containers

**Mobile Optimizations:**
- Reduce code digit size to 36px
- Stack transfer details vertically
- Full-width buttons
- Simplified file list (name + size only)

---

## Trust & Security Visual Cues

- Lock icons accompany password-protected transfers
- Green success indicators for active transfers
- Yellow/orange warnings for near-expiration
- Expiry countdown prominently displayed
- Password strength indicator (if password set)
- Encrypted badge/label for secure transfers

This design creates a professional, trustworthy file transfer experience that balances functionality with modern aesthetics, ensuring data teams can share files efficiently and securely.