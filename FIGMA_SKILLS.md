# 🎨 Figma Skills Guide: Designing Salesforce Screens with SLDS

A comprehensive guide to mastering Figma design for Salesforce applications using the Salesforce Lightning Design System (SLDS).

**Repo:** [SamtasticUI/SFdesign-system](https://github.com/SamtasticUI/SFdesign-system)  
**Language Composition:** JavaScript (65%), SCSS (22.3%), MDX (12.2%)

---

## 📚 Table of Contents

1. [Getting Started](#getting-started)
2. [Essential Skills](#essential-skills)
3. [Component Library Setup](#component-library-setup)
4. [Design Tokens & Variables](#design-tokens--variables)
5. [Building Salesforce Screens](#building-salesforce-screens)
6. [Advanced Techniques](#advanced-techniques)
7. [Design-to-Code Workflow](#design-to-code-workflow)
8. [Best Practices](#best-practices)
9. [Troubleshooting](#troubleshooting)
10. [Resources & Checklists](#resources--checklists)

---

## Getting Started

### Prerequisites
- Figma account (free or paid)
- Access to [SLDS Documentation](https://www.lightningdesignsystem.com)
- This repository cloned locally
- Node.js v14+ for running Storybook

### Step 1: Install Required Figma Plugins (5 minutes)

1. **Figma Tokens** (by Jan Six)
   - Essential for managing design tokens
   - Syncs with code tokens
   - [Install Plugin](https://www.figma.com/community/plugin/843461159747178978/Figma-Tokens)

2. **CSS Exporter**
   - Automatically exports Figma properties to CSS
   - [Install Plugin](https://www.figma.com/community/plugin/767296957564353725/CSS-Exporter)

3. **Wireframe Assistant**
   - Quick prototyping and layout
   - [Install Plugin](https://www.figma.com/community/plugin/782568788843756181/Wireframe-Assistant)

4. **Color Contrast Checker**
   - WCAG accessibility compliance
   - [Install Plugin](https://www.figma.com/community/plugin/748533339900865323/Contrast)

### Step 2: Set Up Your File Structure

```
Salesforce-App-Design/
├── 01_Foundations/
│   ├── Colors
│   ├── Typography
│   ├── Spacing & Grids
│   └── Iconography
├── 02_Components/
│   ├── Buttons
│   ├── Inputs & Forms
│   ├── Navigation
│   ├── Modals
│   ├── Cards
│   ├── Tables
│   └── Lists
├── 03_Screens/
│   ├── List Views
│   ├── Detail Views
│   ├── Forms
│   └── Dashboards
├── 04_Interactions/
│   ├── Prototypes
│   ├── Micro-interactions
│   └── Animations
└── 05_Handoff/
    ├── Developer Notes
    ├── Component Specs
    └── CSS Mapping
```

### Step 3: Import SLDS Design Tokens

1. Go to **Plugins → Figma Tokens**
2. Set up tokens from `design-tokens/tokens.json` (in this repo)
3. Create a local token set with:
   - **Colors:** Primary, Secondary, Neutral, Status (success/error/warning)
   - **Typography:** Font families (Salesforce Sans), sizes, weights
   - **Spacing:** 4px-based scale (xs, sm, md, lg, xl, xxl, xxxl)
   - **Shadows:** Depth levels (1-8)

---

## Essential Skills

### Skill 1: Using Design Tokens

**What:** Design tokens are reusable design decisions (colors, spacing, fonts) stored as variables.

**Why:** Ensures consistency across all screens and simplifies updates.

**How:**

```
Color Token: slds-color-background-primary
├── Light: #FFFFFF
├── Dark: #F3F3F3
└── Hover: #E8E8E8

Spacing Token: slds-spacing-medium
├── Value: 16px
└── Usage: Margins, padding, gaps

Typography Token: slds-font-body-regular
├── Font: Salesforce Sans
├── Size: 14px
├── Weight: 400
└── Line-height: 1.5
```

**Practice Exercise:**
1. Create a simple button in Figma
2. Apply the token for `slds-color-button-brand` (blue)
3. Change the token value globally
4. Notice all buttons update automatically ✓

---

### Skill 2: Creating Reusable Components

**What:** Components in Figma are like HTML elements—reusable building blocks.

**Why:** Faster design, easier updates, consistency.

**How to Create a Button Component:**

1. **Draw the shape**
   ```
   Rectangle: 120px × 44px
   Fill: #0070D2 (Brand Blue)
   Border-radius: 4px
   ```

2. **Add text**
   ```
   Text: "Click Me"
   Font: Salesforce Sans, 14px, Weight 500
   Color: #FFFFFF
   Alignment: Center
   ```

3. **Create variants for states**
   - Default
   - Hover (darker blue)
   - Active (even darker)
   - Disabled (gray)
   - Focus (outline + inner shadow)

4. **Make it a component**
   - Right-click → "Create component"
   - Name: `Button/Primary` (use `/` for grouping)
   - Set main component

5. **Create variants**
   ```
   Component "Button"
   ├── Primary/Default
   ├── Primary/Hover
   ├── Primary/Active
   ├── Primary/Disabled
   ├── Secondary/Default
   ├── Secondary/Hover
   └── ... (add all state combinations)
   ```

**Component Instance Usage:**
```
Drag component onto canvas → Modify instance → Change variant
All instances linked to main component auto-update
```

---

### Skill 3: Building Forms

**What:** Forms are the most common pattern in Salesforce apps.

**Why:** Data entry is critical for CRM applications.

**Structure:**

```html
<!-- Form Anatomy -->
<form class="slds-form">
  <div class="slds-form-element">
    <!-- Label -->
    <label class="slds-form-element__label">
      <abbr class="slds-required" title="required">*</abbr>
      Field Name
    </label>
    
    <!-- Input -->
    <div class="slds-form-element__control">
      <input type="text" class="slds-input" placeholder="Enter value"/>
    </div>
    
    <!-- Help Text -->
    <small class="slds-form-element__help">
      Helpful information here
    </small>
    
    <!-- Error Message -->
    <div class="slds-form-element__error" role="alert">
      Error: This field is required
    </div>
  </div>
</form>
```

**In Figma:**

1. Create input field components:
   - Default state (placeholder text)
   - Focus state (blue border, shadow)
   - Filled state (with content)
   - Error state (red border, error icon)
   - Disabled state (gray)

2. Group with label + help text

3. Create form variations:
   - Required fields (red asterisk)
   - Optional fields
   - With error messages
   - With inline validation

4. Use 8px grid for vertical spacing between fields

---

### Skill 4: Creating Lists and Tables

**What:** Display multiple records with sorting, filtering, pagination.

**Why:** Core feature of Salesforce list views.

**List View Structure:**

```
┌─────────────────────────────────────┐
│  Header                       Filters│
├─────────────────────────────────────┤
│ ☐ Name      | Status  | Created    │
├─────────────────────────────────────┤
│ ☐ Record 1  | Active  | 2024-01-15 │
│ ☐ Record 2  | Active  | 2024-01-14 │
│ ☐ Record 3  | Inactive| 2024-01-13 │
├─────────────────────────────────────┤
│ Showing 3 of 250  [< 1 2 3 > ]      │
└─────────────────────────────────────┘
```

**Figma Table Component:**

1. **Create table row component**
   ```
   Row Height: 44px
   Columns: Checkbox | Name | Status | Date | Actions
   Padding: 8px
   Border-bottom: 1px #E8E8E8
   ```

2. **Cell variants**
   - Text cell
   - Status badge cell (Active/Inactive/Pending)
   - Action menu cell (...)
   - Link cell (clickable)

3. **Row states**
   - Default
   - Hover (light gray background)
   - Selected (darker background)
   - Focus (outline)

4. **Add header row**
   ```
   Header: Bold font, darker background (#F3F3F3)
   Sort indicators (↑↓ icons)
   Drag to reorder columns
   ```

5. **Add pagination component**
   ```
   "Showing 1-10 of 250 items"
   [< Previous] [1] [2] [3] [Next >]
   ```

---

### Skill 5: Building Modals

**What:** Overlays that focus user attention on a specific task.

**Why:** Confirmation dialogs, forms, alerts in Salesforce.

**Modal Anatomy:**

```
┌──────────────────────────────────────┐
│ Header            Close Icon (✕)     │
├──────────────────────────────────────┤
│                                      │
│           Modal Content              │
│           (Form, message, etc)       │
│                                      │
├──────────────────────────────────────┤
│ Cancel Button    Save Button (Primary)│
└──────────────────────────────────────┘
Backdrop (semi-transparent dark overlay)
```

**In Figma:**

1. **Create modal frame**
   ```
   Width: 500px (adjust for content)
   Height: Auto (expands with content)
   Background: #FFFFFF
   Border-radius: 4px
   Box-shadow: 0 10px 40px rgba(0,0,0,0.2)
   ```

2. **Add components**
   - Header (16px padding, bold text)
   - Close button (top-right, 24×24px)
   - Content area (24px padding)
   - Footer with action buttons (spacing between)

3. **Create backdrop**
   ```
   Full-screen rectangle behind modal
   Background: rgba(0,0,0,0.5)
   Interaction: Click to close
   ```

4. **Modal variants**
   - Confirmation (question icon, 2 buttons)
   - Success (checkmark icon, 1 button)
   - Error (alert icon, 1-2 buttons)
   - Form (inputs, submit button)

---

## Component Library Setup

### Organization Strategy

```
Components (main file)
│
├── Buttons
│   ├── Button (main component)
│   │   ├── Primary/Default
│   │   ├── Primary/Hover
│   │   ├── Primary/Active
│   │   ├── Primary/Disabled
│   │   ├── Secondary/...
│   │   └── Destructive/...
│   └── Icon Button
│
├── Forms
│   ├── Input Field
│   │   ├── Text/Default
│   │   ├── Text/Focus
│   │   ├── Text/Error
│   │   └── Text/Disabled
│   ├── Select Dropdown
│   ├── Checkbox
│   ├── Radio
│   └── Toggle Switch
│
├── Navigation
│   ├── Top Navigation Bar
│   ├── Sidebar Navigation
│   └── Breadcrumb
│
├── Data Display
│   ├── Table
│   ├── List Item
│   ├── Card
│   ├── Badge
│   └── Pill
│
├── Feedback
│   ├── Alert
│   ├── Toast
│   ├── Spinner
│   └── Skeleton
│
└── Modals
    ├── Modal Container
    ├── Modal Header
    └── Modal Footer
```

### Naming Conventions

**Formula:** `Category / ComponentName / Variant / State`

**Examples:**
```
Buttons/Button Primary/Default
Buttons/Button Primary/Hover
Buttons/Button Primary/Disabled
Forms/Input Text/Default
Forms/Input Text/Focus
Forms/Input Text/Error
Navigation/Top Bar/Light
Data Display/Table Row/Default
Data Display/Table Row/Hover
Data Display/Table Row/Selected
```

### Documentation in Figma

1. **Create a "Guidelines" page**
   - Component usage rules
   - Do's and Don'ts
   - When to use each variant

2. **Add descriptions to components**
   - Right-click component → Edit component
   - Add description with guidelines
   - Include CSS class names

3. **Link to Storybook**
   - Add links in notes: [View in Storybook](http://localhost:9002)
   - Live interactive examples for developers

---

## Design Tokens & Variables

### Setting Up Figma Tokens

**1. Install Figma Tokens Plugin**

**2. Create token structure**

```json
{
  "Global": {
    "Colors": {
      "Primary": { "value": "#0070D2" },
      "Success": { "value": "#04844B" },
      "Warning": { "value": "#FFC220" },
      "Error": { "value": "#C23030" },
      "Neutral": { "value": "#E8E8E8" }
    },
    "Typography": {
      "FontFamily": { "value": "Salesforce Sans" },
      "Size": {
        "Small": { "value": "12px" },
        "Regular": { "value": "14px" },
        "Large": { "value": "16px" },
        "XLarge": { "value": "18px" }
      },
      "Weight": {
        "Regular": { "value": "400" },
        "Medium": { "value": "500" },
        "Bold": { "value": "700" }
      }
    },
    "Spacing": {
      "XS": { "value": "4px" },
      "Small": { "value": "8px" },
      "Medium": { "value": "16px" },
      "Large": { "value": "24px" },
      "XLarge": { "value": "32px" }
    },
    "Shadow": {
      "Level1": {
        "value": "0 2px 4px rgba(0,0,0,0.1)"
      },
      "Level2": {
        "value": "0 4px 8px rgba(0,0,0,0.15)"
      }
    }
  }
}
```

**3. Apply tokens to components**

- Select element
- In Figma Tokens panel
- Click token to apply

**4. Sync with code** (Advanced)

- Export tokens to JSON
- Import into component library
- Variables auto-sync across design and code

---

## Building Salesforce Screens

### Screen 1: Account List View

**Objective:** Display paginated list of accounts with sorting and filtering.

**Layout:**
```
┌─────────────────────────────────────────────────────┐
│ Accounts                                    [+ New] │
├─────────────────────────────────────────────────────┤
│ Search [________]     Filter ▼    View ▼            │
├─────────────────────────────────────────────────────┤
│ ☐ Name         | Type      | Phone       | Revenue  │
├─────────────────────────────────────────────────────┤
│ ☐ Acme Corp    | Customer  | 555-1234    | $1.2M   │
│ ☐ TechStart    | Partner   | 555-5678    | $500K   │
│ ☐ Global Ltd   | Prospect  | 555-9012    | $2.1M   │
│ ☐ Innovation   | Customer  | 555-3456    | $750K   │
├─────────────────────────────────────────────────────┤
│ Showing 4 of 127                [< 1 2 3 > ]       │
└─────────────────────────────────────────────────────┘
```

**Step-by-step in Figma:**

1. **Create header section**
   - Title: "Accounts" (24px, bold)
   - Action button: "[+ New Account]" (primary button style)

2. **Create toolbar**
   - Search input (with magnifying glass icon)
   - Filter button (dropdown)
   - View selector (dropdown)
   - Spacing: 16px between elements

3. **Create table**
   - Use table row component from component library
   - 4 columns: Checkbox | Name | Type | Phone | Revenue
   - Add 4 rows of sample data
   - Alternating row colors (every other row slightly gray) improves readability

4. **Add pagination**
   - Status: "Showing 4 of 127"
   - Page buttons: 1, 2, 3 (current page highlighted)
   - Previous/Next arrows

5. **Add interactions** (Prototyping)
   - Filter button → Shows filter panel
   - Row click → Opens detail view
   - Sort arrow → Re-sorts column

---

### Screen 2: Contact Form

**Objective:** Multi-field form with validation and error states.

**Layout:**
```
┌─────────────────────────────────────┐
│ New Contact                    ✕    │
├─────────────────────────────────────┤
│                                     │
│ First Name *                        │
│ [___________________]               │
│                                     │
│ Last Name *                         │
│ [___________________]               │
│                                     │
│ Email                               │
│ [___________________]               │
│  ⚠ Invalid email format             │
│                                     │
│ Phone                               │
│ [___________________]               │
│                                     │
│ Account *                           │
│ [Select Account      ▼]             │
│                                     │
│         [Cancel]  [Save]            │
└─────────────────────────────────────┘
```

**Figma Steps:**

1. **Create form container (modal)**
   - 500px width
   - Auto height
   - 24px padding

2. **Create form sections**
   - Group 1: First Name, Last Name (2 columns)
   - Group 2: Email (with error state shown)
   - Group 3: Phone
   - Group 4: Account selector (dropdown)

3. **Input field variants**
   - Show 3 states:
     - Default (empty placeholder)
     - Focus (blue border, cursor)
     - Error (red border, error icon, error message)

4. **Footer buttons**
   - Cancel (secondary button)
   - Save (primary button)
   - Spacing: 12px between buttons, right-aligned

5. **Add validation indicators**
   - Red asterisk (*) for required fields
   - Error icon (!) for invalid fields
   - Error message in red text below field

---

### Screen 3: Record Detail View

**Objective:** Display record details with edit mode.

**View Mode:**
```
┌────────────────────────────────────────┐
│ Account                        [Edit] │
├────────────────────────────────────────┤
│                                        │
│ Name: Acme Corporation                 │
│ Account Number: ACC-2024-001           │
│ Type: Customer                         │
│ Industry: Technology                   │
│ Annual Revenue: $1,200,000             │
│                                        │
│ Contact Information                    │
│ Phone: (555) 123-4567                  │
│ Website: www.acmecorp.com              │
│ Email: contact@acmecorp.com            │
│                                        │
│ Related Records (6)                    │
│ ┌─ Contact 1                          │
│ ├─ Contact 2                          │
│ └─ Contact 3                          │
│                                        │
└────────────────────────────────────────┘
```

**Edit Mode:**
```
┌────────────────────────────────────────┐
│ Account                [Save] [Cancel] │
├────────────────────────────────────────┤
│                                        │
│ Name *                                 │
│ [Acme Corporation        ]             │
│                                        │
│ Account Number                         │
│ [ACC-2024-001           ]              │
│                                        │
│ Type *                                 │
│ [Customer              ▼]              │
│                                        │
│ Industry                               │
│ [Technology            ▼]              │
│                                        │
│         [Save]  [Cancel]               │
└────────────────────────────────────────┘
```

**Figma Steps:**

1. **Create two frames:** "Detail_View" and "Detail_Edit"

2. **View Mode:**
   - Field labels (bold, 14px)
   - Field values (regular, 14px)
   - Edit button (top-right)
   - Dividers between sections

3. **Edit Mode:**
   - Replace values with input fields
   - Add Save/Cancel buttons
   - Change Edit button to Save/Cancel

4. **Add section headers**
   - "Contact Information" (16px, bold, light gray background)
   - Padding: 16px

5. **Related records section**
   - Mini list of related contacts
   - Each item is clickable (hover state)
   - "View all (6)" link at bottom

---

## Advanced Techniques

### 1. Creating Responsive Designs

**Desktop (1440px):**
```
┌─────────────┬──────────────────────┐
│   Sidebar   │   Main Content       │
│  (200px)    │      (1240px)        │
└─────────────┴──────────────────────┘
```

**Tablet (768px):**
```
┌─────────────┬──────────────────┐
│  Sidebar    │  Content         │
│  (150px)    │  (618px)         │
└─────────────┴──────────────────┘
```

**Mobile (375px):**
```
┌───────────────────┐
│ Hamburger Menu    │
├───────────────────┤
│  Main Content     │
│  (Full Width)     │
└───────────────────┘
```

**Figma Approach:**

1. Create 3 separate frames (Desktop, Tablet, Mobile)
2. Use same components but reposition
3. Add constraints to responsive elements
4. Document breakpoints in prototype

### 2. Interactive Prototypes

**Setup:**

1. Select element
2. Click **Prototype** tab (right panel)
3. Add interaction:
   - Trigger: `On click`
   - Action: `Navigate to [Screen Name]`
   - Animation: `Smart animate` (smooth transitions)

**Example Flows:**
```
List View (Row Click)
  → Detail View

Detail View (Edit Button)
  → Edit Mode (same frame)

Form (Submit)
  → Success Modal
  → Back to List View

Filter Button
  → Filter Panel
  → Apply → Filtered List
```

### 3. Micro-interactions

**Hover States:**
```
Button Default
  [Hover] → Button Hover (darker blue, shadow)
  [Click] → Button Active (even darker)
```

**Loading States:**
```
Form Default
  [Submit Click] → Loading State (spinner in button)
  [Delay 2s] → Success Modal
```

**Validation Feedback:**
```
Email Input (Typing)
  [Invalid format] → Error state (red border, icon)
  [Valid format] → Success state (green icon, no border)
```

---

## Design-to-Code Workflow

### Step 1: Design Specifications

**In Figma, document for each component:**

```
Component: Button - Primary
├── Dimensions: 120px W × 44px H
├── Colors:
│   ├── Default: #0070D2 (brand-blue)
│   ├── Hover: #0056B4 (brand-blue-dark)
│   ├── Active: #003A7A (brand-blue-darker)
│   └── Disabled: #CCCCCC (neutral-gray)
├── Typography:
│   ├── Font: Salesforce Sans
│   ├── Size: 14px
│   ├── Weight: 500
│   └── Color: #FFFFFF
├── Spacing:
│   ├── Padding: 0 16px (horizontal)
│   ├── Padding: 8px 0 (vertical)
│   └── Border-radius: 4px
├── States: Default, Hover, Active, Disabled, Focus
└── SLDS Classes: slds-button slds-button_brand
```

### Step 2: Export Specifications

**Use CSS Exporter Plugin:**

1. Select component
2. Right-click → "Export to CSS"
3. Generate CSS file
4. Copy class names

**Manual method:**
```css
.slds-button {
  padding: 8px 16px;
  font-size: 14px;
  font-weight: 500;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.2s;
}

.slds-button_brand {
  background-color: #0070D2;
  color: #FFFFFF;
}

.slds-button_brand:hover {
  background-color: #0056B4;
}

.slds-button_brand:active {
  background-color: #003A7A;
}

.slds-button:disabled {
  background-color: #CCCCCC;
  cursor: not-allowed;
}
```

### Step 3: Component Mapping

**Reference:** `formats/figma/components-mapping.json`

```json
{
  "component": "Button",
  "figma_variant": "Primary",
  "slds_classes": {
    "default": "slds-button slds-button_brand",
    "hover": "slds-button slds-button_brand",
    "active": "slds-button slds-button_brand slds-is-active",
    "disabled": "slds-button slds-button_brand slds-is-disabled"
  },
  "html_example": "<button class='slds-button slds-button_brand'>Click Me</button>"
}
```

### Step 4: Developer Handoff

**Create handoff document:**

1. **Component specs** (dimensions, colors, spacing)
2. **SLDS class mapping** (exact classes to use)
3. **State variations** (all states + interactions)
4. **Links to:**
   - Storybook: http://localhost:9002
   - SLDS Docs: https://www.lightningdesignsystem.com
   - This repo: https://github.com/SamtasticUI/SFdesign-system

**Example Handoff:**

```markdown
## Button Component

### Figma File
[Link to Figma component]

### SLDS Classes
- Primary: `slds-button slds-button_brand`
- Secondary: `slds-button slds-button_neutral`
- Destructive: `slds-button slds-button_destructive`

### CSS Variables (from design-tokens)
- Color: `var(--slds-color-button-brand)`
- Padding: `var(--slds-spacing-medium)`
- Font-size: `var(--slds-font-size-regular)`

### States
- Default, Hover, Active, Disabled, Focus

### Storybook Link
http://localhost:9002/?path=/story/buttons--primary

### Implementation
See `ui/components/Button.js` in repository
```

---

## Best Practices

### Do's ✅

- **Use the grid**: Align to 4px/8px grid for precision
- **Organize layers**: Clean layer names (not "Group 1", use "Header")
- **Document everything**: Add descriptions, notes, links
- **Test accessibility**: Use color contrast checker (4.5:1 minimum)
- **Keep components updated**: Single source of truth
- **Use design tokens**: Colors, spacing, fonts from variables
- **Version control**: Keep Figma link in GitHub
- **Prototype interactions**: Show click targets and transitions
- **Test responsiveness**: Design all breakpoints
- **Follow SLDS guidelines**: Maintain consistency with Salesforce

### Don'ts ❌

- **Don't create duplicate components**: Use variants instead
- **Don't ignore accessibility**: Test with color-blind simulators
- **Don't hardcode values**: Always use tokens/variables
- **Don't forget mobile**: Design mobile-first or at minimum
- **Don't overload pages**: Keep wireframes clear and readable
- **Don't use unclear names**: Use semantic naming (not "box_blue_2")
- **Don't mix design systems**: Stick with SLDS only
- **Don't ignore spacing rhythm**: Be consistent with 4px/8px grid
- **Don't skip documentation**: Future you will thank present you
- **Don't hide related components**: Group similar items together

### Accessibility Checklist

**Color & Contrast:**
- [ ] Color contrast ≥ 4.5:1 for regular text
- [ ] Color contrast ≥ 3:1 for large text
- [ ] Don't use color alone to convey meaning (use icons, labels)
- [ ] Test with color-blind simulator (Red Colorblind, Blue-Yellow)

**Typography:**
- [ ] Minimum font size: 12px (14px recommended)
- [ ] Line height: ≥ 1.5
- [ ] Letter spacing adequate for readability
- [ ] Sufficient contrast between text and background

**Interactive Elements:**
- [ ] Touch targets ≥ 44px × 44px
- [ ] Clear focus states (visible outline/highlight)
- [ ] Hover states visually distinct
- [ ] Disabled states clearly marked

**Forms:**
- [ ] All inputs have associated labels
- [ ] Required fields marked with * (explain: "* = required")
- [ ] Error messages clear and specific
- [ ] Error icon + color + text (not color alone)

**Navigation:**
- [ ] Current page clearly highlighted
- [ ] Logical tab order
- [ ] Keyboard accessible (all elements reachable)

---

## Troubleshooting

### Problem 1: Components Not Updating Across Instances

**Symptom:** Changed main component but instances didn't update.

**Solutions:**
1. Ensure main component is actually selected (blue icon)
2. Check if instances are "detached" (right-click → "Detach instance")
3. Refresh page (Cmd+R / Ctrl+R)
4. Relink detached instances to main component

---

### Problem 2: Design Tokens Not Syncing

**Symptom:** Changed token value in plugin but Figma didn't update.

**Solutions:**
1. Verify token set is active (Figma Tokens → Select set)
2. Ensure element is actually using token (not hardcoded color)
3. Try "Push all tokens" button in plugin
4. Restart Figma

---

### Problem 3: Prototype Links Not Working

**Symptom:** Prototype preview shows blank screen or wrong frame.

**Solutions:**
1. Verify destination frame exists and is marked as "Prototype"
2. Check trigger and action settings (On click → Navigate to...)
3. Ensure target frame is visible in prototype settings
4. Try "Copy prototype link" and paste in new tab

---

### Problem 4: Responsive Layout Breaking on Mobile

**Symptom:** Elements overlap or disappear on small screens.

**Solutions:**
1. Use Figma constraints (right panel → Constraints)
2. Set elements to "scale with parent" or "fixed width"
3. Create separate mobile frame (don't resize desktop)
4. Test all breakpoints: 375px, 768px, 1440px

---

### Problem 5: Performance Issues with Large Files

**Symptom:** Figma is slow, laggy, or freezes.

**Solutions:**
1. Archive unused pages/frames
2. Remove unnecessary groups and layers
3. Use components instead of copied elements
4. Reduce number of shapes (use strokes instead of shapes)
5. Split into multiple files (foundation, components, screens)

---

### Problem 6: SLDS Classes Not Matching Figma Design

**Symptom:** Developer implemented SLDS classes but it looks different.

**Solutions:**
1. Verify correct SLDS version (check `package.json`)
2. Check if custom CSS is overriding SLDS
3. Ensure all required parent classes are applied
4. Compare with Storybook: http://localhost:9002
5. Update Figma design to match actual SLDS implementation

---

## Resources & Checklists

### Helpful Links

**SLDS Resources:**
- [Salesforce Lightning Design System](https://www.lightningdesignsystem.com)
- [SLDS Storybook](http://localhost:9002) - Run `npm start` first
- [SLDS GitHub Repository](https://github.com/salesforce-ux/design-system)
- [SLDS Components Mapping](./formats/figma/components-mapping.json) - In this repo

**Figma Learning:**
- [Figma Design Systems Guide](https://www.figma.com/design-systems/)
- [Figma Plugins Directory](https://www.figma.com/community/plugins)
- [Figma Best Practices](https://help.figma.com/hc/en-us/sections/4405269689243-Best-practices)

**Plugins We Use:**
- [Figma Tokens](https://www.figma.com/community/plugin/843461159747178978/Figma-Tokens)
- [CSS Exporter](https://www.figma.com/community/plugin/767296957564353725/CSS-Exporter)
- [Wireframe Assistant](https://www.figma.com/community/plugin/782568788843756181/Wireframe-Assistant)
- [Contrast](https://www.figma.com/community/plugin/748533339900865323/Contrast)

**Accessibility:**
- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [Color Blindness Simulator](https://www.color-blindness.com/coblis-color-blindness-simulator/)
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)

---

### Pre-Design Checklist

Before starting a new screen design:

- [ ] Understand the business requirement
- [ ] Map user flows and interactions
- [ ] Identify SLDS components needed
- [ ] Create wireframe/low-fidelity sketch
- [ ] Review component library for existing patterns
- [ ] Plan responsive breakpoints (mobile, tablet, desktop)
- [ ] Identify form fields and validation states
- [ ] Plan error messages and edge cases
- [ ] Ensure accessibility compliance
- [ ] Schedule design review with team

---

### Component Design Checklist

For each component created:

- [ ] All states documented (default, hover, active, disabled, focus)
- [ ] Naming follows convention: `Category/Component/Variant/State`
- [ ] Main component properly set up
- [ ] Variants created for all necessary combinations
- [ ] Accessibility requirements met (contrast, sizing)
- [ ] Design tokens applied (colors, spacing, typography)
- [ ] Aligned to 4px/8px grid
- [ ] Layer organization clean and logical
- [ ] Description added with SLDS class names
- [ ] Links added to Storybook and documentation

---

### Handoff Checklist

Before handing off to developers:

- [ ] All screens completed and reviewed
- [ ] Components properly named and organized
- [ ] Design tokens exported and documented
- [ ] SLDS class mapping completed
- [ ] CSS specifications generated
- [ ] Prototypes with interactions created
- [ ] Responsive designs for all breakpoints
- [ ] Accessibility verified (colors, contrast, sizing)
- [ ] Documentation and notes added
- [ ] Links to code repository and Storybook included
- [ ] Version control: Figma link in GitHub README

---

### Post-Launch Checklist

After implementation:

- [ ] Design matches Figma as closely as possible
- [ ] All states and interactions working
- [ ] Responsive design works on all devices
- [ ] Accessibility requirements met (color, focus, etc)
- [ ] Performance is acceptable
- [ ] Cross-browser compatibility verified
- [ ] Update Figma if discrepancies found
- [ ] Document any design-to-code decisions
- [ ] Archive old design files
- [ ] Plan next iteration based on user feedback

---

## Quick Reference

### SLDS Color Tokens

```
Primary: #0070D2 (Blue)
Secondary: #F3F3F3 (Light Gray)
Success: #04844B (Green)
Warning: #FFC220 (Yellow)
Error: #C23030 (Red)
Info: #0070D2 (Blue)
Neutral: #E8E8E8 (Gray)
Text: #000000 (Black)
Text Muted: #626262 (Dark Gray)
```

### SLDS Spacing Scale (4px-based)

```
Extra Small (xs): 4px
Small (sm): 8px
Medium (md): 16px
Large (lg): 24px
Extra Large (xl): 32px
Extra Extra Large (xxl): 48px
Extra Extra Extra Large (xxxl): 64px
```

### SLDS Typography

```
Font Family: Salesforce Sans, Arial, sans-serif
Heading 1: 28px, 700 weight, 1.4 line-height
Heading 2: 24px, 700 weight, 1.4 line-height
Heading 3: 20px, 700 weight, 1.4 line-height
Body: 14px, 400 weight, 1.5 line-height
Body Small: 12px, 400 weight, 1.5 line-height
```

### Common SLDS Classes

```
Buttons: slds-button, slds-button_brand, slds-button_neutral, slds-button_destructive
Forms: slds-form, slds-form-element, slds-form-element__control, slds-input
Tables: slds-table, slds-table_fixed-layout, slds-table_striped
Modals: slds-modal, slds-modal_large, slds-modal_small, slds-backdrop
Alerts: slds-notify, slds-notify_alert, slds-alert_success, slds-alert_error
Navigation: slds-nav-vertical, slds-nav-vertical_compact, slds-nav-horizontal
```

---

## Getting Help

**Questions about this guide?**
- Open an issue: [GitHub Issues](https://github.com/SamtasticUI/SFdesign-system/issues)
- Check Storybook: http://localhost:9002

**Questions about SLDS?**
- Visit: https://www.lightningdesignsystem.com
- Read docs: https://www.lightningdesignsystem.com/guidelines/overview/

**Questions about Figma?**
- Help Center: https://help.figma.com
- Community: https://www.figma.com/community

---

**Last Updated:** 2026-05-26  
**Repository:** [SamtasticUI/SFdesign-system](https://github.com/SamtasticUI/SFdesign-system)  
**Language Composition:** JavaScript (65%), SCSS (22.3%), MDX (12.2%)

Happy designing! 🎨
