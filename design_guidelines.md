# PC Club Time Calculator - Design Guidelines

## Design Approach
**Reference-Based**: Drawing inspiration from modern dashboard applications like Linear, Vercel Dashboard, and gaming-oriented UIs that combine minimalism with striking visual elements.

## Core Design Principles
- **Gaming-Inspired Minimalism**: Clean, focused interface with strategic gaming aesthetic touches
- **Dark-First Experience**: Deep dark background with high contrast for readability in dimly lit PC club environments
- **Instant Clarity**: All pricing information immediately visible and comprehensible at a glance

## Typography
**Font Families**:
- Primary: 'Inter' (Google Fonts) - weights 400, 500, 600, 700
- Accent/Numbers: 'JetBrains Mono' (Google Fonts) - weight 500, 600 for pricing and time displays

**Hierarchy**:
- Page title: text-3xl/4xl font-bold
- Section headers: text-xl/2xl font-semibold
- Tariff names: text-lg font-semibold
- Body text: text-base font-medium
- Prices/Numbers: text-2xl/3xl font-mono font-semibold
- Helper text: text-sm font-normal

## Layout System
**Spacing Primitives**: Tailwind units of 2, 4, 6, 8, 12, 16
- Component padding: p-6 to p-8
- Section gaps: gap-6 to gap-8
- Card spacing: space-y-4
- Maximum container width: max-w-4xl

## Component Library

### Navigation/Header
- Compact top bar with logo/title on left
- Live clock display (HH:MM format) on right showing current time
- Day type indicator (Будни/Выходные) with subtle badge styling

### Calculator Card
- Large central card (rounded-2xl) containing all calculator functionality
- Divided into clear sections with subtle dividers
- Tariff selection as prominent cards/buttons in grid layout (grid-cols-2)
- Each tariff card displays: name, duration, description, weekday/weekend prices side-by-side

### Time Input Section
- Clean numeric input for minutes/hours
- Real-time price calculation display beneath input
- Visual feedback showing tariff being applied
- Rounded final price prominently displayed

### Price Display Components
- Monospace font for all numerical values
- Price cards with clear weekday/weekend distinction
- Current active price highlighted with cyan-blue glow effect
- Strikethrough on inactive pricing option

### Tariff Cards
- Grid layout (2 columns on desktop, 1 on mobile)
- Each card contains: tariff icon/badge, name, duration info, dual pricing
- Hover state with subtle border glow in cyan-blue
- Active/selected state with stronger cyan-blue border and background tint

## Color Palette Structure
- **Background**: Deep dark (near black)
- **Cards/Surfaces**: Elevated dark grey (lighter than background)
- **Primary Accent**: Cyan-blue for interactive elements, highlights, and active states
- **Text Primary**: Near white for high contrast
- **Text Secondary**: Medium grey for descriptions
- **Success/Calculation**: Cyan-blue glow for final prices
- **Borders**: Subtle grey, accent cyan-blue for interactive states

## Icons
**Library**: Heroicons (via CDN)
- Clock icon for time displays
- Calendar icon for weekday/weekend indicator
- Gaming controller or trophy icons for tariff badges
- Calculator icon in header

## Responsive Behavior
- Desktop (lg:): Two-column tariff grid, side-by-side price comparisons
- Mobile (base): Single column stack, vertically aligned pricing
- Consistent padding scaling: p-4 mobile → p-8 desktop

## Special Features
- **Live Time Integration**: Real-time clock in header updates every minute
- **Auto-calculation**: Prices update instantly as user types duration
- **Cyber Night Restriction**: Visual indication when tariff is/isn't available based on current time
- **Rounding Indicator**: Subtle text showing "rounded up from X.XX" when applicable

## Animations
- Minimal, purposeful only:
  - Smooth price number transitions when calculations update
  - Subtle pulse on currently selected tariff
  - Gentle fade-in for calculation results

## Accessibility
- High contrast text against dark backgrounds
- Clear visual hierarchy with consistent spacing
- Keyboard navigation for tariff selection and inputs
- ARIA labels for time displays and price calculations

**Note**: No hero image needed - this is a utility calculator focused on function and clarity.