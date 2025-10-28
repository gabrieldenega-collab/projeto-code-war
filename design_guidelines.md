# Corporate Ledger (CLEG) Design Guidelines

## Design Approach
**Reference-Based Approach**: Drawing from leading FinTech platforms like Stripe, Coinbase, and Robinhood for clean, trust-building interfaces with futuristic blockchain aesthetics.

## Core Design Principles
- **Futuristic FinTech Minimalism**: Clean, professional, high-end financial technology aesthetic
- **Trust & Transparency**: Clear hierarchy, readable data presentation, institutional credibility
- **Blockchain Visual Language**: Subtle hexagonal patterns, digital connecting lines, network motifs as background elements

## Color System
- **Primary**: Dark Navy Blue (#0A1128) - main backgrounds, headers
- **Secondary**: Graphite Gray (#2C3E50) - cards, secondary sections
- **Accent/CTA**: Electric Green/Cyan (#00FFC2, #00C2FF) - buttons, highlights, interactive elements
- **Text**: White for primary text, light gray for secondary content
- **Data Visualization**: Use accent colors for charts and graphs

## Typography
- **Font Families**: Montserrat for headings (bold, large), Inter or Roboto for body text
- **Hierarchy**: 
  - Hero Headlines: 48-64px, bold
  - Section Titles: 32-40px, bold
  - Card Titles: 20-24px, semi-bold
  - Body Text: 16-18px, regular
  - Data/Numbers: Tabular figures, bold for emphasis

## Layout System
**Spacing**: Use Tailwind units of 4, 6, 8, 12, 16, 24 for consistent rhythm (p-4, p-8, p-12, py-16, py-24)

## Images
**Hero Section**: Full-width background image of modern skyscrapers/commercial buildings with digital overlay effects (hexagons, network lines). Apply dark gradient overlay (0.4-0.6 opacity) for text readability.

**Asset Cards**: High-quality photos of modern commercial buildings, professional architectural photography style.

**How It Works Section**: Use custom illustrations or minimalist icons representing each step.

## Component Library

### Navigation Header
- Dark background with glass morphism effect
- Logo (CLEG) left-aligned
- Horizontal menu: Home, Ativos, Dashboard, White Paper, Contato
- Login/Cadastro button (accent color, prominent)
- Sticky on scroll with subtle blur backdrop

### Hero Section (Landing Page)
- Full viewport height with background image
- Centered content: Large headline + sub-headline + primary CTA
- CTA button with blurred background, accent color border and text
- Floating card overlay showing key stats (Total Volume, Tokens Available)

### Benefits Section (3 Blocks)
- Horizontal grid layout (3 columns desktop, stacked mobile)
- Each block: Icon (60-80px), Title (bold), Description
- Icons: Minimalist line style, accent color
- Subtle hover effect: lift and glow

### How It Works Section
- Numbered steps (1-2-3-4) with connecting line
- Each step: Large number, icon, title, brief description
- Flow visualization with accent-colored connecting elements

### Market Data Section
- Bold statistics in large format
- Counters with accent color highlights
- Source citations in smaller text
- Background: Subtle hexagonal pattern overlay

### Asset Cards (Marketplace)
- Card style: Graphite gray background, subtle rounded corners (8-12px)
- Image: Building photo at top (16:9 ratio)
- Content: Property name, location, price per token (large, bold), tokens remaining (progress bar), estimated APY
- CTA button: "Comprar Tokens" (accent color)
- Hover: Subtle lift effect, accent border glow

### Dashboard Components
- **Portfolio Table**: Clean data table with alternating row backgrounds, clear column headers
- **Distribution Chart**: Donut or pie chart using accent color gradients
- **Recent Yields List**: Transaction cards with date, amount (bold, accent color), asset name
- **Summary Cards**: Total value, tokens owned, total yields - large numbers with labels

### Forms (Login/Buy)
- Input fields: Dark background, light border, focus state with accent glow
- Validation states: Green for success, red for errors
- Submit buttons: Full-width on mobile, accent color with hover states

### Footer
- Multi-column layout: Logo + about, Quick Links, Legal, Social
- Dark background matching header
- Subtle divider lines between sections

## Interactions & Animations
- **Hover States**: Subtle scale (1.02-1.05), accent color glow, smooth transitions (300ms)
- **Loading States**: Skeleton screens with shimmer effect
- **Page Transitions**: Smooth fade-ins for content sections
- **Data Updates**: Pulsing effect for real-time number changes
- **Scroll Triggers**: Fade-up animations for sections as they enter viewport

## Responsive Breakpoints
- Mobile: <768px - single column, stacked navigation
- Tablet: 768-1024px - 2 column grids
- Desktop: >1024px - full multi-column layouts, expanded navigation

## Accessibility
- High contrast ratios for all text
- Focus indicators for keyboard navigation (accent color outline)
- ARIA labels for interactive elements
- Alt text for all images

## Mobile-First Considerations
- Touch-friendly button sizes (minimum 44x44px)
- Simplified navigation menu (hamburger)
- Card-based layouts for easy scrolling
- Larger text for readability on small screens
- Bottom-anchored CTAs for thumb accessibility