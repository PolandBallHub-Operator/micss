# micss
ux library for html

# Micss - Mi-like UI CSS Framework

Micss is a lightweight CSS/UI framework built on a Mi-like design language. It focuses on flat-solid aesthetics, borderless card containers, dynamic CSS custom properties via the PTZ standard, and smooth elastic overscroll animations.

---

## 🚀 Key Features

1. **Divider-Free Solid UI**
   - Eliminates outer borders and internal dividing lines for a clean, minimalist visual presentation.
   - Single HTML is recommended. This will allow for faster delivery.
2. **PTZ Dynamic Engine Integration**
   - Uses CSS custom properties (`:root` variables) to dynamically update UI metrics—including card border radius, thick slider height, and toggle switch dimensions—in real time.
3. **Elastic Overscroll Animation**
   - Built-in rubber-band bounce effects for touch gestures and mouse wheel scrolling at top and bottom bounds.
4. **Seamless Dark Mode Sync**
   - Automatic switching and synchronization with system dark mode preferences or manual toggles.

---

## 📦 File Structure

```text
micss/
├── index.html       # Primary application entry point & component gallery
└── README.md        # Documentation
```

---

## 🛠️ Core Components & CSS Classes

### 1. Card Container (`.glass-card`)
A solid background card using dynamic border radius (`--ptz-card-radius`).

```html
<div class="glass-card">
    <h2>Card Title</h2>
    <p>Card content goes here...</p>
</div>
```

> **Design Constraint:** Nesting gray cards inside white cards is strictly prohibited.

---

### 2. List Components (`.custom-list`, `.list-item`)
Divider-free list layout designed for flat visual hierarchy.

```html
<div class="custom-list">
    <div class="list-item">
        <div>
            <div class="list-item-title">Item Title</div>
            <div class="list-item-desc">Item description</div>
        </div>
        <button class="ai-btn">Action</button>
    </div>
</div>
```

---

### 3. Action Buttons (`.ai-btn`, `.ai-btn-secondary`)
Rounded buttons utilizing primary accent colors or neutral secondary background states.

```html
<!-- Primary Button -->
<button class="ai-btn">Action</button>

<!-- Secondary Button -->
<button class="ai-btn ai-btn-secondary">Cancel</button>
```

---

### 4. Toggle Switch (`.switch`, `.slider`)
Custom animated switch built using CSS custom properties.

```html
<label class="switch">
    <input type="checkbox" checked>
    <span class="slider"></span>
</label>
```

---

### 5. Custom Thick Slider (`.thick-slider-container`, `.thick-slider-fill`)
A touch-friendly thick slider component with filled progress visualization.

```html
<div class="slider-wrapper">
    <div class="slider-label-row">
        <span>Setting Name</span>
        <span id="val-label">50%</span>
    </div>
    <div class="thick-slider-container">
        <div class="thick-slider-fill" id="slider-fill" style="width: 50%;">
            <div class="thick-slider-knob"></div>
        </div>
        <input type="range" class="thick-slider-input" min="0" max="100" value="50" oninput="handleParamChange(...)">
    </div>
</div>
```

---

### 6. Input Field (`.glass-input`)
Simple, rounded input element for text input.

```html
<div class="glass-input-wrapper">
    <input type="text" class="glass-input" placeholder="Enter text...">
</div>
```

---

### 7. Fixed Bottom Navigation (`.bottom-nav-container`, `.nav-item`)
Fixed bottom navigation bar adhering to Mi-like design specifications.

```html
<div class="bottom-nav-container">
    <div class="nav-item active" onclick="switchView('view-catalog')">
        <span class="material-symbols-outlined">style</span>
        <span class="nav-label">Catalog</span>
    </div>
</div>
```

---

## ⚙️ PTZ JSON Specification

Dynamic UI parameters can be exported or imported in bulk via `PTZ.json`.

### Schema Example

```json
{
  "themeName": "ShowMeCSS Default Blue",
  "accentColor": "#3381FF",
  "cardRadius": 24,
  "sliderHeight": 25,
  "toggleWidth": 54,
  "toggleHeight": 30,
  "toggleKnobRadius": 50,
  "toggleKnobWidth": 22,
  "bgLight": "#F7F7F7",
  "bgDark": "#121212"
}
```

---

## 📝 Design & Development Guidelines

1. **No cdn CSS:** Use native CSS custom properties (`:root`) and standard stylesheets.
2. **Preserve Component Class Names:** Keep base class names (`.glass-card`, `.ai-btn`, `.switch`, `.thick-slider-container`, etc.) intact.
3. **Card Hierarchy Rules:** Do not nest dark/gray sub-cards within primary white card containers.
4. **Mi-like Naming Convention:** Always refer to the design language as "Mi-like". Do not use "X****i".
5. **No Phone Frames:** Designed strictly for standard web app viewports. Do not enclose the layout in mobile device frames.
6. **Content Guidelines:** When creating applications (e.g., Countryball / Polandball apps), avoid political satire, sarcasm, or offensive slang (such as *kurwa* or *anschluss*) to maintain an accessible experience for all users.
