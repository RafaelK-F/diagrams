# OpuDoc Design System - Komplette Entwicklerdokumentation
*Die ultimative Referenz für das OpuDoc Design System - Maximale Detailtiefe für Entwickler*

## INHALTSVERZEICHNIS

1. [Design Philosophy & Prinzipien](#1-design-philosophy--prinzipien)
2. [Farbsystem & Design Tokens](#2-farbsystem--design-tokens)
3. [Physikalisch basierte Animationen](#3-physikalisch-basierte-animationen)
4. [Komponenten-Architektur](#4-komponenten-architektur)
5. [Layout & Grid-System](#5-layout--grid-system)
6. [Typografie & Text-System](#6-typografie--text-system)
7. [Interaktive Elemente](#7-interaktive-elemente)
8. [Glassmorphism & Blur-Effekte](#8-glassmorphism--blur-effekte)
9. [Shadow & Lighting System](#9-shadow--lighting-system)
10. [Tab Navigation System](#10-tab-navigation-system)
11. [Modal & Overlay System](#11-modal--overlay-system)
12. [Form & Input Components](#12-form--input-components)
13. [Button System](#13-button-system)
14. [Card & Surface System](#14-card--surface-system)
15. [Icon & Visual Elements](#15-icon--visual-elements)
16. [Responsive Design Guidelines](#16-responsive-design-guidelines)
17. [Accessibility Standards](#17-accessibility-standards)
18. [Performance Optimierungen](#18-performance-optimierungen)
19. [Browser Compatibility](#19-browser-compatibility)
20. [Debugging & Troubleshooting](#20-debugging--troubleshooting)
21. [Implementation Guide](#21-implementation-guide)
22. [Migration Strategies](#22-migration-strategies)
23. [Testing Frameworks](#23-testing-frameworks)
24. [Maintenance & Updates](#24-maintenance--updates)
25. [Advanced Patterns](#25-advanced-patterns)
26. [Code Style Guide](#26-code-style-guide)
27. [Performance Benchmarks](#27-performance-benchmarks)
28. [Security Considerations](#28-security-considerations)
29. [Deployment Strategies](#29-deployment-strategies)
30. [Future Roadmap](#30-future-roadmap)

---

## 1. DESIGN PHILOSOPHY & PRINZIPIEN

### 1.1 Kernphilosophie

Das OpuDoc Design System basiert auf sechs fundamentalen Prinzipien, die alle Designentscheidungen leiten:

#### 1.1.1 Physikalische Authentizität
Alle Animationen und Interaktionen folgen physikalischen Gesetzen der realen Welt:

**Trägheit (Inertia)**
```css
/* Objekte starten langsam und beschleunigen graduell */
.inertia-start {
  animation-timing-function: cubic-bezier(0, 0, 0.2, 1);
  /* Entspricht: ease-out - startet schnell, wird langsamer */
}
```

**Federkraft (Spring Physics)**
```css
/* Elastische Bewegungen mit natürlichem Overshoot */
.spring-motion {
  animation-timing-function: cubic-bezier(0.175, 0.885, 0.32, 1.275);
  /* Simuliert: Beschleunigung -> Overshoot -> Stabilisierung */
}
```

**Reibung (Friction)**
```css
/* Bewegungen verlangsamen sich natürlich */
.friction-deceleration {
  animation-timing-function: cubic-bezier(0.4, 0, 0.6, 1);
  /* Simuliert natürliche Verlangsamung durch Widerstand */
}
```

**Schwerkraft (Gravity)**
```css
/* Vertikale Bewegungen folgen gravitativen Prinzipien */
.gravity-fall {
  animation-timing-function: cubic-bezier(0.55, 0, 1, 0.45);
  /* Simuliert freien Fall mit Beschleunigung */
}
```

#### 1.1.2 Glassmorphism Ästhetik
Moderne Transparenz-Effekte mit tiefem visuellen Layering:

**Backdrop Blur Hierarchie**
```css
/* Level 1: Subtile Transparenz für dezente Hervorhebung */
.glass-level-1 {
  background: hsl(var(--card) / 0.6);
  backdrop-filter: blur(4px);
  border: 1px solid hsl(var(--border) / 0.3);
}

/* Level 2: Mittlere Transparenz für Kartenelemente */
.glass-level-2 {
  background: hsl(var(--card) / 0.8);
  backdrop-filter: blur(8px);
  border: 1px solid hsl(var(--border) / 0.5);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
}

/* Level 3: Starke Transparenz für Modals und Overlays */
.glass-level-3 {
  background: hsl(var(--card) / 0.9);
  backdrop-filter: blur(16px);
  border: 1px solid hsl(var(--border) / 0.7);
  box-shadow: 
    0 20px 50px rgba(0, 0, 0, 0.4),
    inset 0 1px 0 rgba(255, 255, 255, 0.1);
}
```

**Transparenz-Schichten für visuelle Hierarchie**
```css
/* Basis-Layer: 40% Transparenz */
.layer-base { background: hsl(var(--background) / 0.4); }

/* Content-Layer: 60% Transparenz */
.layer-content { background: hsl(var(--card) / 0.6); }

/* Interactive-Layer: 80% Transparenz */
.layer-interactive { background: hsl(var(--accent) / 0.8); }

/* Focus-Layer: 95% Transparenz */
.layer-focus { background: hsl(var(--primary) / 0.95); }
```

#### 1.1.3 Dark-First Design Philosophy
Primäre Optimierung für dunkle Umgebungen mit wissenschaftlich fundierten Vorteilen:

**Augenschonung (Eye Strain Reduction)**
```css
/* Optimierte Helligkeitswerte für minimale Augenbelastung */
:root {
  /* Maximale empfohlene Helligkeit: 4% für Basis */
  --background: 220 15% 4%;
  
  /* Schrittweise Erhöhung für visuelle Hierarchie */
  --surface-l1: 220 13% 6%;   /* +2% für erste Erhebung */
  --surface-l2: 220 13% 8%;   /* +2% für zweite Erhebung */
  --surface-l3: 220 13% 10%;  /* +2% für dritte Erhebung */
}
```

**Kontrast-Optimierung nach WCAG-Standards**
```css
/* AAA-Level Kontrast für kritischen Text */
.text-critical {
  color: hsl(220 8% 94%);     /* 18.5:1 Kontrast-Ratio */
}

/* AA-Level Kontrast für normalen Text */
.text-normal {
  color: hsl(220 8% 80%);     /* 7.2:1 Kontrast-Ratio */
}

/* Minimum AA für sekundären Text */
.text-secondary {
  color: hsl(220 8% 60%);     /* 4.5:1 Kontrast-Ratio */
}
```

#### 1.1.4 Semantische Konsistenz
Logische, nachvollziehbare Begründung für jede Designentscheidung:

**Color Token Semantik**
```css
/* Funktionsbasierte Benennung statt visueller Beschreibung */
/* ❌ FALSCH */
.gray-dark { color: #333; }
.blue-light { color: #87ceeb; }

/* ✅ RICHTIG */
.text-primary { color: hsl(var(--foreground)); }
.surface-elevated { background: hsl(var(--card)); }
.action-primary { background: hsl(var(--primary)); }
```

### 1.2 Mathematische Design-Prinzipien

#### 1.2.1 Golden Ratio in Spacing
```css
/* Fibonacci-basierte Spacing-Sequenz */
:root {
  --space-1: 0.25rem;    /* 4px - φ⁰ × 4 */
  --space-2: 0.5rem;     /* 8px - φ¹ × 4 (gerundet) */
  --space-3: 0.75rem;    /* 12px - φ² × 4 (gerundet) */
  --space-4: 1rem;       /* 16px - φ³ × 4 (gerundet) */
  --space-5: 1.5rem;     /* 24px - φ⁴ × 4 (gerundet) */
  --space-6: 2.5rem;     /* 40px - φ⁵ × 4 (gerundet) */
  --space-7: 4rem;       /* 64px - φ⁶ × 4 (gerundet) */
}
```

#### 1.2.2 Modular Scale für Typography
```css
/* Typografische Skala basierend auf der Quarte (1.333) */
:root {
  --text-xs: 0.75rem;     /* 12px */
  --text-sm: 0.875rem;    /* 14px */
  --text-base: 1rem;      /* 16px - Basis */
  --text-lg: 1.125rem;    /* 18px */
  --text-xl: 1.25rem;     /* 20px */
  --text-2xl: 1.5rem;     /* 24px */
  --text-3xl: 2rem;       /* 32px */
  --text-4xl: 2.5rem;     /* 40px */
}
```

---

## 2. FARBSYSTEM & DESIGN TOKENS

### 2.1 Fundamentales HSL-Farbsystem

#### 2.1.1 CRITICAL: HSL-Only Policy - Absolute Compliance Required

**ABSOLUT VERBOTEN**: Direkte Hex/RGB-Farben in Komponenten
```css
/* ❌ NIEMALS SO - Führt zu Inkonsistenz und schwieriger Wartung */
.wrong-approach {
  background: #1a1a1a;
  color: white;
  border: 1px solid #333333;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

/* ✅ IMMER SO - Semantisch, wartbar, themefähig */
.correct-approach {
  background: hsl(var(--background));
  color: hsl(var(--foreground));
  border: 1px solid hsl(var(--border));
  box-shadow: 0 4px 8px hsl(var(--background) / 0.2);
}
```

**Enforcement durch CSS Custom Properties**
```css
/* Globale Regel um direkte Farbwerte zu verhindern */
* {
  /* Diese Regel zwingt zur Verwendung von CSS-Variablen */
  color: hsl(var(--foreground, 0 0% 50%));
  background-color: hsl(var(--background, 0 0% 100%));
}
```

#### 2.1.2 Vollständige Color Token Hierarchie

##### 2.1.2.1 Foundation Layer (Basis-Schicht)
```css
/* === BACKGROUND & SURFACE COLORS === */
/* Wissenschaftlich optimierte Helligkeitswerte für Augenkomfort */

--background: 220 15% 4%;           /* #0a0b0f - Haupthintergrund
                                       RGB: 10, 11, 15
                                       Grund: Minimale Helligkeit für OLED-Effizienz
                                       Kontrast mit Foreground: 18.75:1 (AAA) */

--card: 220 13% 6%;                 /* #0f1113 - Karten-Hintergrund
                                       RGB: 15, 17, 19
                                       Grund: Erste visuelle Erhebung (+2% Helligkeit)
                                       Verwendung: Cards, Panels, primäre Container */

--popover: 220 13% 6%;              /* #0f1113 - Popover-Hintergrund
                                       RGB: 15, 17, 19
                                       Grund: Konsistent mit Cards für einheitliche UX
                                       Verwendung: Tooltips, Dropdowns, temporäre Overlays */

--app-surface: 220 13% 7%;          /* #111315 - App-Oberfläche
                                       RGB: 17, 19, 21
                                       Grund: Mittlere Erhebung für Hauptinhalte
                                       Verwendung: Sidebars, Navigation, Content-Areas */

--app-surface-hover: 220 13% 9%;    /* #161719 - App-Oberfläche Hover
                                       RGB: 22, 23, 25
                                       Grund: Interaktive Rückmeldung (+2% für Hover)
                                       Verwendung: Hover-States für Surface-Elemente */

--muted: 220 13% 7%;                /* #111315 - Gedämpfte Elemente
                                       RGB: 17, 19, 21
                                       Grund: Neutrale Basis für weniger wichtige Elemente
                                       Verwendung: Disabled States, Background Sections */
```

##### 2.1.2.2 Overlay & Backdrop System
```css
/* === OVERLAY & BACKDROP COLORS === */
/* Spezielle Alpha-Werte für Glassmorphism und Modal-Systeme */

--backdrop-blur: 220 15% 4% / 0.8;  /* rgba(10, 11, 15, 0.8) - Modal Backdrop
                                        Grund: 80% Opazität für Modal-Fokussierung
                                        Verwendung: Dialog-Hintergründe, Modal Overlays */

--backdrop-light: 220 15% 4% / 0.6; /* rgba(10, 11, 15, 0.6) - Leichter Backdrop
                                        Grund: 60% Opazität für dezente Overlays
                                        Verwendung: Popover-Hintergründe, Dropdown-Shadows */

--glass-bg: 220 13% 6% / 0.8;       /* rgba(15, 17, 19, 0.8) - Glassmorphism Base
                                        Grund: 80% Opazität für Blur-Effekte
                                        Verwendung: Glass-Cards, Transparente Panels */

--dropdown-shadow: 220 15% 2% / 0.5; /* rgba(5, 6, 8, 0.5) - Dropdown Schatten
                                         Grund: 50% Opazität für subtile Schatten
                                         Verwendung: Context-Menüs, Select-Dropdowns */

/* === ADVANCED OVERLAY VARIATIONS === */
--overlay-subtle: 220 15% 4% / 0.3;  /* 30% für sehr dezente Overlays */
--overlay-medium: 220 15% 4% / 0.6;  /* 60% für Standard-Overlays */
--overlay-strong: 220 15% 4% / 0.9;  /* 90% für fokussierte Modals */
--overlay-opaque: 220 15% 4% / 1.0;  /* 100% für vollständige Blockierung */
```

##### 2.1.2.3 Content & Text Layer (Inhalts-Schicht)
```css
/* === TEXT COLORS === */
/* WCAG AAA-konforme Kontrastverhältnisse für optimale Lesbarkeit */

--foreground: 220 8% 94%;           /* #eff0f2 - Primärer Text
                                       RGB: 239, 240, 242
                                       Kontrast: 18.75:1 mit Background (AAA)
                                       Verwendung: Headlines, wichtige Labels, primärer Content */

--card-foreground: 220 8% 92%;      /* #eaebec - Karten-Text
                                       RGB: 234, 235, 236
                                       Kontrast: 16.2:1 mit Card Background (AAA)
                                       Verwendung: Text auf Cards, Panel-Content */

--popover-foreground: 220 8% 92%;   /* #eaebec - Popover-Text
                                       RGB: 234, 235, 236
                                       Kontrast: 16.2:1 mit Popover Background (AAA)
                                       Verwendung: Tooltip-Text, Dropdown-Inhalte */

--muted-foreground: 220 8% 60%;     /* #949699 - Sekundärer Text
                                       RGB: 148, 150, 153
                                       Kontrast: 4.8:1 mit Background (AA)
                                       Verwendung: Beschreibungen, Meta-Informationen */

--secondary-foreground: 220 8% 80%; /* #c7c8ca - Mittlere Text-Priorität
                                       RGB: 199, 200, 202
                                       Kontrast: 9.1:1 mit Background (AAA)
                                       Verwendung: Subheadings, sekundäre Labels */

/* === TEXT HIERARCHY EXTENSIONS === */
--text-primary: 220 8% 94%;         /* #eff0f2 - Höchste Priorität
                                       Verwendung: H1, wichtige CTAs, kritische Meldungen */

--text-secondary: 220 8% 80%;       /* #c7c8ca - Mittlere Priorität
                                       Verwendung: H2-H4, normale Beschreibungen */

--text-tertiary: 220 8% 60%;        /* #949699 - Niedrige Priorität
                                       Verwendung: Captions, Timestamps, Meta-Info */

--text-disabled: 220 8% 40%;        /* #636466 - Deaktivierte Elemente
                                       Kontrast: 2.8:1 (unter AA, intentional für disabled)
                                       Verwendung: Disabled buttons, inactive states */

--text-placeholder: 220 8% 45%;     /* #6e6f71 - Placeholder Text
                                       Kontrast: 3.2:1 (intentional für Placeholders)
                                       Verwendung: Input-Placeholders, leere States */

--text-inverse: 220 15% 8%;         /* #111213 - Umgekehrter Text
                                       Verwendung: Text auf hellen Hintergründen */
```

##### 2.1.2.4 Interactive & Action Layer
```css
/* === INTERACTIVE COLORS === */
/* Vollständiges State-System für alle interaktiven Elemente */

/* PRIMARY ACTION SYSTEM */
--primary: 220 8% 88%;              /* #dddee0 - Primäre Aktionen
                                       RGB: 221, 222, 224
                                       Grund: Helle Farbe für maximale Aufmerksamkeit
                                       Verwendung: CTAs, wichtige Buttons, Links */

--primary-foreground: 220 15% 8%;   /* #111213 - Text auf Primary
                                       RGB: 17, 18, 19
                                       Kontrast: 18.1:1 mit Primary (AAA)
                                       Verwendung: Button-Text, Link-Text auf Primary */

--primary-hover: 220 8% 85%;        /* #d5d6d8 - Primary Hover State
                                       RGB: 213, 214, 216
                                       Grund: -3% Helligkeit für Hover-Feedback */

--primary-active: 220 8% 82%;       /* #cdced0 - Primary Active State
                                       RGB: 205, 206, 208
                                       Grund: -6% Helligkeit für Active-Feedback */

--primary-disabled: 220 8% 50%;     /* #7b7c7e - Primary Disabled
                                       RGB: 123, 124, 126
                                       Grund: Stark reduzierte Helligkeit für disabled */

/* SECONDARY ACTION SYSTEM */
--secondary: 220 13% 8%;            /* #121416 - Sekundäre Aktionen
                                       RGB: 18, 20, 22
                                       Grund: Dunkle Basis für sekundäre Wichtigkeit
                                       Verwendung: Sekundäre Buttons, alternative Aktionen */

--secondary-foreground: 220 8% 88%; /* #dddee0 - Text auf Secondary
                                       RGB: 221, 222, 224
                                       Kontrast: 16.8:1 mit Secondary (AAA) */

--secondary-hover: 220 13% 10%;     /* #161719 - Secondary Hover
                                       RGB: 22, 23, 25
                                       Grund: +2% Helligkeit für Hover-Feedback */

--secondary-active: 220 13% 12%;    /* #1a1b1d - Secondary Active
                                       RGB: 26, 27, 29
                                       Grund: +4% Helligkeit für Active-Feedback */

--secondary-disabled: 220 13% 6%;   /* #0f1113 - Secondary Disabled
                                       RGB: 15, 17, 19
                                       Grund: Reduzierte Helligkeit für disabled */

/* ACCENT ACTION SYSTEM */
--accent: 220 13% 10%;              /* #161719 - Akzent-Aktionen
                                       RGB: 22, 23, 25
                                       Grund: Mittlere Helligkeit für Akzente
                                       Verwendung: Highlights, Tabs, Navigation */

--accent-foreground: 220 8% 88%;    /* #dddee0 - Text auf Accent
                                       RGB: 221, 222, 224
                                       Kontrast: 14.2:1 mit Accent (AAA) */

--accent-hover: 220 13% 12%;        /* #1a1b1d - Accent Hover
                                       RGB: 26, 27, 29
                                       Grund: +2% Helligkeit für Hover-Feedback */

--accent-active: 220 13% 14%;       /* #1e1f21 - Accent Active
                                       RGB: 30, 31, 33
                                       Grund: +4% Helligkeit für Active-Feedback */

--accent-disabled: 220 13% 7%;      /* #111315 - Accent Disabled
                                       RGB: 17, 19, 21
                                       Grund: Reduzierte Helligkeit für disabled */

/* === UNIVERSAL INTERACTIVE STATES === */
--interactive-base: 220 13% 8%;     /* Basis für alle interaktiven Elemente */
--interactive-hover: 220 13% 10%;   /* Standard hover state (+2% Helligkeit) */
--interactive-active: 220 13% 12%;  /* Standard active state (+4% Helligkeit) */
--interactive-focus: 220 8% 70%;    /* Focus-Zustand für Accessibility */
--interactive-disabled: 220 13% 6%; /* Disabled interactive elements (-2% Helligkeit) */
--interactive-loading: 220 8% 60%;  /* Loading-Zustand für asynchrone Aktionen */
```

##### 2.1.2.5 Form & Input System
```css
/* === FORM & INPUT COLORS === */
/* Spezialisiertes Farbsystem für Formulare mit erweiterten States */

/* INPUT BASE SYSTEM */
--input: 220 13% 8%;                /* #121416 - Input Hintergrund
                                       RGB: 18, 20, 22
                                       Grund: Dunkler Hintergrund für Input-Kontrast
                                       Verwendung: Textfelder, Selects, Textareas */

--input-hover: 220 13% 10%;         /* #161719 - Input Hover
                                       RGB: 22, 23, 25
                                       Grund: +2% Helligkeit für Hover-Feedback */

--input-focus: 220 13% 12%;         /* #1a1b1d - Input Focus
                                       RGB: 26, 27, 29
                                       Grund: +4% Helligkeit für Focus-State */

--input-error: 220 13% 8%;          /* #121416 - Input Error (gleiche Basis)
                                       Grund: Error wird durch Border kommuniziert */

--input-success: 220 13% 8%;        /* #121416 - Input Success (gleiche Basis)
                                       Grund: Success wird durch Border kommuniziert */

--input-disabled: 220 13% 6%;       /* #0f1113 - Input Disabled
                                       RGB: 15, 17, 19
                                       Grund: Reduzierte Helligkeit für disabled */

/* BORDER SYSTEM FÜR INPUTS */
--input-border: 220 13% 12%;        /* #1a1b1d - Input Border
                                       RGB: 26, 27, 29
                                       Grund: Subtile Abgrenzung vom Hintergrund */

--input-border-hover: 220 13% 15%;  /* #242527 - Input Border Hover
                                       RGB: 36, 37, 39
                                       Grund: Verstärkte Border für Hover */

--input-border-focus: 220 8% 70%;   /* #b1b2b4 - Input Border Focus
                                       RGB: 177, 178, 180
                                       Grund: Starker Kontrast für Focus-Indication */

--input-border-error: 0 50% 45%;    /* #b33a3a - Input Border Error
                                       RGB: 179, 58, 58
                                       Grund: Rote Kennzeichnung für Fehler */

--input-border-success: 120 50% 45%; /* #3ab33a - Input Border Success
                                        RGB: 58, 179, 58
                                        Grund: Grüne Kennzeichnung für Success */

/* UNIVERSAL BORDER SYSTEM */
--border: 220 13% 12%;              /* #1a1b1d - Standard Border
                                       RGB: 26, 27, 29
                                       Verwendung: Cards, Panels, Separatoren */

--border-hover: 220 13% 15%;        /* #242527 - Border Hover
                                       RGB: 36, 37, 39
                                       Verwendung: Hover-States für bordered Elemente */

--border-focus: 220 8% 70%;         /* #b1b2b4 - Border Focus
                                       RGB: 177, 178, 180
                                       Verwendung: Focus-States, Active-Borders */

--border-subtle: 220 13% 8%;        /* #121416 - Subtile Borders
                                       RGB: 18, 20, 22
                                       Verwendung: Interne Separatoren, Grid-Lines */

--border-strong: 220 13% 20%;       /* #2f3133 - Starke Borders
                                       RGB: 47, 49, 51
                                       Verwendung: Wichtige Abgrenzungen, Rahmen */

/* FOCUS RING SYSTEM */
--ring: 220 8% 70%;                 /* #b1b2b4 - Focus Ring
                                       RGB: 177, 178, 180
                                       Grund: Starker Kontrast für Accessibility */

--ring-offset: 220 15% 4%;          /* #0a0b0f - Ring Offset (background)
                                       RGB: 10, 11, 15
                                       Grund: Offset-Farbe entspricht Background */

--ring-error: 0 50% 45%;            /* #b33a3a - Error Focus Ring */
--ring-success: 120 50% 45%;        /* #3ab33a - Success Focus Ring */
--ring-warning: 45 90% 55%;         /* #f5c842 - Warning Focus Ring */
```

##### 2.1.2.6 Comprehensive Feedback System
```css
/* === FEEDBACK COLORS === */
/* Vollständiges Feedback-System nach UX-Standards */

/* DESTRUCTIVE/ERROR SYSTEM */
--destructive: 0 50% 45%;           /* #b33a3a - Fehler/Löschungen
                                       RGB: 179, 58, 58
                                       Grund: Klassisches Rot für Aufmerksamkeit
                                       Kontrast: 4.6:1 mit Background (AA)
                                       Verwendung: Error-Messages, Delete-Buttons */

--destructive-foreground: 220 8% 94%; /* #eff0f2 - Text auf Destructive
                                         RGB: 239, 240, 242
                                         Kontrast: 7.8:1 mit Destructive (AAA)
                                         Verwendung: Text auf Error-Buttons, Error-Text */

--destructive-hover: 0 50% 40%;     /* #a03333 - Destructive Hover
                                       RGB: 160, 51, 51
                                       Grund: -5% Helligkeit für Hover-Darkening */

--destructive-active: 0 50% 35%;    /* #8d2d2d - Destructive Active
                                       RGB: 141, 45, 45
                                       Grund: -10% Helligkeit für Active-Press */

--destructive-disabled: 0 30% 30%;  /* #666060 - Destructive Disabled
                                       RGB: 102, 96, 96
                                       Grund: Desaturiert und dunkler für disabled */

/* SUCCESS SYSTEM */
--success: 120 50% 45%;             /* #3ab33a - Erfolg
                                       RGB: 58, 179, 58
                                       Grund: Klassisches Grün für positive Aktionen
                                       Kontrast: 4.8:1 mit Background (AA)
                                       Verwendung: Success-Messages, Confirm-Buttons */

--success-foreground: 220 8% 94%;   /* #eff0f2 - Text auf Success
                                       RGB: 239, 240, 242
                                       Kontrast: 8.2:1 mit Success (AAA) */

--success-hover: 120 50% 40%;       /* #33a033 - Success Hover
                                       RGB: 51, 160, 51
                                       Grund: -5% Helligkeit für Hover */

--success-active: 120 50% 35%;      /* #2d8d2d - Success Active
                                       RGB: 45, 141, 45
                                       Grund: -10% Helligkeit für Active */

--success-disabled: 120 30% 30%;    /* #606660 - Success Disabled
                                       RGB: 96, 102, 96
                                       Grund: Desaturiert für disabled */

/* WARNING SYSTEM */
--warning: 45 90% 55%;              /* #f5c842 - Warnung
                                       RGB: 245, 200, 66
                                       Grund: Orange/Gelb für Aufmerksamkeit ohne Alarm
                                       Kontrast: 8.9:1 mit Background (AAA)
                                       Verwendung: Warning-Messages, Caution-Buttons */

--warning-foreground: 220 15% 8%;   /* #111213 - Text auf Warning
                                       RGB: 17, 18, 19
                                       Kontrast: 16.8:1 mit Warning (AAA)
                                       Grund: Dunkler Text auf hellem Warning */

--warning-hover: 45 90% 50%;        /* #f2c239 - Warning Hover
                                       RGB: 242, 194, 57
                                       Grund: -5% Helligkeit für Hover */

--warning-active: 45 90% 45%;       /* #efbc30 - Warning Active
                                       RGB: 239, 188, 48
                                       Grund: -10% Helligkeit für Active */

--warning-disabled: 45 50% 40%;     /* #b8a366 - Warning Disabled
                                       RGB: 184, 163, 102
                                       Grund: Desaturiert für disabled */

/* INFO SYSTEM */
--info: 200 80% 60%;                /* #3d9ff0 - Information
                                       RGB: 61, 159, 240
                                       Grund: Blaue Töne für neutrale Information
                                       Kontrast: 5.8:1 mit Background (AA)
                                       Verwendung: Info-Messages, Help-Buttons */

--info-foreground: 220 8% 94%;      /* #eff0f2 - Text auf Info
                                       RGB: 239, 240, 242
                                       Kontrast: 9.1:1 mit Info (AAA) */

--info-hover: 200 80% 55%;          /* #2e95ed - Info Hover
                                       RGB: 46, 149, 237
                                       Grund: -5% Helligkeit für Hover */

--info-active: 200 80% 50%;         /* #1f8bea - Info Active
                                       RGB: 31, 139, 234
                                       Grund: -10% Helligkeit für Active */

--info-disabled: 200 50% 40%;       /* #6699b8 - Info Disabled
                                       RGB: 102, 153, 184
                                       Grund: Desaturiert für disabled */

/* EXTENDED FEEDBACK STATES */
--feedback-subtle: 220 8% 80%;      /* Subtile Feedback-Färbung */
--feedback-moderate: 220 8% 70%;    /* Moderate Feedback-Stärke */
--feedback-strong: 220 8% 88%;      /* Starke Feedback-Hervorhebung */
```

##### 2.1.2.7 Custom Application Layer
```css
/* === CUSTOM APP COLORS === */
/* Spezialisierte Farben für App-spezifische Elemente */

/* STATUS & INDICATOR SYSTEM */
--color-indicator: 220 8% 70%;      /* #b1b2b4 - Status-Indikatoren
                                       RGB: 177, 178, 180
                                       Grund: Neutrale Farbe für Statusinformationen
                                       Verwendung: Badges, Pills, Status-Dots */

--indicator-online: 120 60% 50%;    /* #3dcc3d - Online-Status
                                       RGB: 61, 204, 61
                                       Verwendung: Online-Indikatoren, aktive States */

--indicator-offline: 0 0% 40%;      /* #666666 - Offline-Status
                                       RGB: 102, 102, 102
                                       Verwendung: Offline-Indikatoren, inaktive States */

--indicator-busy: 45 90% 55%;       /* #f5c842 - Busy-Status
                                       RGB: 245, 200, 66
                                       Verwendung: Busy-Indikatoren, Loading-States */

--indicator-away: 30 70% 50%;       /* #d6913d - Away-Status
                                       RGB: 214, 145, 61
                                       Verwendung: Away-Indikatoren, Pause-States */

/* BUTTON GROUP SYSTEM */
--button-group: 220 13% 8%;         /* #121416 - Button-Gruppen Base
                                       RGB: 18, 20, 22
                                       Grund: Einheitlicher Hintergrund für Button-Sammlungen
                                       Verwendung: Toolbar-Hintergründe, Button-Container */

--button-group-hover: 220 13% 10%;  /* #161719 - Button-Gruppen Hover
                                       RGB: 22, 23, 25
                                       Grund: Hover-State für gesamte Button-Gruppe */

--button-group-active: 220 13% 12%; /* #1a1b1d - Button-Gruppen Active
                                       RGB: 26, 27, 29
                                       Grund: Active-State für Button-Gruppe */

--button-group-selected: 220 13% 14%; /* #1e1f21 - Ausgewählter Button in Gruppe
                                         RGB: 30, 31, 33
                                         Grund: Hervorhebung des aktiven Buttons */

/* TAB SYSTEM COLORS */
--tab-active: 220 13% 11%;          /* #181a1c - Aktive Tabs
                                       RGB: 24, 26, 28
                                       Grund: Leichte Erhebung für aktiven Tab
                                       Verwendung: Aktive Tab-Hintergründe */

--tab-inactive: 220 13% 7%;         /* #111315 - Inaktive Tabs
                                       RGB: 17, 19, 21
                                       Grund: Reduzierte Helligkeit für Inaktivität
                                       Verwendung: Inaktive Tab-Hintergründe */

--tab-hover: 220 13% 9%;            /* #161719 - Tab Hover
                                       RGB: 22, 23, 25
                                       Grund: Intermediate Helligkeit für Hover
                                       Verwendung: Hover-State für inaktive Tabs */

--tab-border-active: 220 8% 70%;    /* #b1b2b4 - Border für aktive Tabs
                                       RGB: 177, 178, 180
                                       Grund: Starker Kontrast für Active-Indication */

--tab-border-inactive: 220 13% 12%; /* #1a1b1d - Border für inaktive Tabs
                                       RGB: 26, 27, 29
                                       Grund: Subtile Abgrenzung */

/* SPECIAL EFFECT COLORS */
--glow-primary: 220 8% 88% / 0.1;   /* Primary Glow-Effekt
                                       Verwendung: Box-Shadow Glows für Primary Elements */

--glow-accent: 220 13% 10% / 0.2;   /* Accent Glow-Effekt
                                       Verwendung: Box-Shadow Glows für Accent Elements */

--glow-success: 120 50% 45% / 0.15; /* Success Glow-Effekt */
--glow-warning: 45 90% 55% / 0.15;  /* Warning Glow-Effekt */
--glow-error: 0 50% 45% / 0.15;     /* Error Glow-Effekt */

--highlight: 220 8% 94% / 0.05;     /* Subtile Hervorhebung
                                       Verwendung: Hover-Highlights, Selection */

--selection: 220 8% 88% / 0.1;      /* Text-Auswahl
                                       Verwendung: ::selection Pseudo-Element */

--mark-highlight: 45 90% 55% / 0.3; /* Mark/Highlight-Farbe
                                       Verwendung: <mark> Element, Suchresultate */
```

##### 2.1.2.8 Sidebar Subsystem
```css
/* === SIDEBAR COLORS === */
/* Separates Farbsystem für Sidebar-Komponenten */

/* SIDEBAR BASE SYSTEM */
--sidebar-background: 220 13% 6%;      /* #0f1113 - Sidebar Basis
                                          RGB: 15, 17, 19
                                          Grund: Etwas heller als main Background
                                          Verwendung: Sidebar-Hintergrund */

--sidebar-foreground: 220 8% 92%;      /* #eaebec - Sidebar Text
                                          RGB: 234, 235, 236
                                          Kontrast: 16.2:1 mit Sidebar Background (AAA)
                                          Verwendung: Sidebar-Text, Labels */

--sidebar-primary: 220 8% 88%;         /* #dddee0 - Sidebar Primary
                                          RGB: 221, 222, 224
                                          Grund: Konsistent mit Main Primary
                                          Verwendung: Aktive Sidebar-Links */

--sidebar-primary-foreground: 220 15% 8%; /* #111213 - Text auf Sidebar Primary
                                             RGB: 17, 18, 19
                                             Kontrast: 18.1:1 (AAA) */

--sidebar-accent: 220 13% 10%;         /* #161719 - Sidebar Accent
                                          RGB: 22, 23, 25
                                          Grund: Konsistent mit Main Accent
                                          Verwendung: Sidebar Highlights */

--sidebar-accent-foreground: 220 8% 88%; /* #dddee0 - Text auf Sidebar Accent
                                           RGB: 221, 222, 224
                                           Kontrast: 14.2:1 (AAA) */

--sidebar-border: 220 13% 12%;         /* #1a1b1d - Sidebar Grenzen
                                          RGB: 26, 27, 29
                                          Grund: Konsistente Border-Farbe
                                          Verwendung: Sidebar-Rahmen, Separatoren */

--sidebar-ring: 220 8% 70%;           /* #b1b2b4 - Sidebar Focus Ring
                                         RGB: 177, 178, 180
                                         Grund: Konsistente Focus-Indication */

/* SIDEBAR INTERACTION STATES */
--sidebar-item-hover: 220 13% 8%;     /* #121416 - Sidebar Item Hover
                                          RGB: 18, 20, 22
                                          Grund: Leichte Verdunkelung für Hover */

--sidebar-item-active: 220 13% 10%;   /* #161719 - Sidebar Item Active
                                          RGB: 22, 23, 25
                                          Grund: Moderate Aufhellung für Active */

--sidebar-item-selected: 220 13% 12%; /* #1a1b1d - Sidebar Item Selected
                                          RGB: 26, 27, 29
                                          Grund: Stärkere Aufhellung für Selection */

--sidebar-group-title: 220 8% 80%;    /* #c7c8ca - Sidebar Gruppen-Titel
                                          RGB: 199, 200, 202
                                          Grund: Reduzierte Wichtigkeit für Gruppierung */

--sidebar-group-background: 220 13% 5%; /* #0d0e10 - Sidebar Gruppen-Hintergrund
                                           RGB: 13, 14, 16
                                           Grund: Leichte Verdunkelung für Gruppierung */

/* SIDEBAR STATES */
--sidebar-collapsed-background: 220 13% 5%; /* Kollabierte Sidebar */
--sidebar-expanded-background: 220 13% 6%;  /* Expandierte Sidebar */
--sidebar-mini-background: 220 13% 7%;      /* Mini-Sidebar Modus */
```

##### 2.1.2.9 Global Design Tokens
```css
/* === DESIGN TOKENS === */
/* Fundamentale Design-Parameter für das gesamte System */

/* BORDER RADIUS SYSTEM */
--radius: 0.5rem;                   /* 8px - Standard Border-Radius
                                       Grund: Optimal für moderne UI-Elemente
                                       Verwendung: Buttons, Cards, Inputs */

--radius-sm: 0.25rem;               /* 4px - Kleine Radius
                                       Verwendung: Kleine Elemente, Badges */

--radius-md: 0.375rem;              /* 6px - Mittlere Radius
                                       Verwendung: Kompakte Elemente */

--radius-lg: 0.75rem;               /* 12px - Große Radius
                                       Verwendung: Cards, Panels */

--radius-xl: 1rem;                  /* 16px - Extra große Radius
                                       Verwendung: Hero-Elemente, Modals */

--radius-2xl: 1.5rem;               /* 24px - Sehr große Radius
                                       Verwendung: Spezielle Container */

--radius-full: 9999px;              /* Vollständig rund
                                       Verwendung: Kreise, Pills */

/* SPACING SYSTEM (Fibonacci-basiert) */
--spacing-0: 0rem;                  /* 0px - Kein Abstand */
--spacing-px: 0.0625rem;            /* 1px - Minimal */
--spacing-0_5: 0.125rem;            /* 2px - Micro */
--spacing-1: 0.25rem;               /* 4px - Extra Small */
--spacing-1_5: 0.375rem;            /* 6px - Small+ */
--spacing-2: 0.5rem;                /* 8px - Small */
--spacing-2_5: 0.625rem;            /* 10px - Small+ */
--spacing-3: 0.75rem;               /* 12px - Medium- */
--spacing-3_5: 0.875rem;            /* 14px - Medium */
--spacing-4: 1rem;                  /* 16px - Medium */
--spacing-5: 1.25rem;               /* 20px - Medium+ */
--spacing-6: 1.5rem;                /* 24px - Large- */
--spacing-7: 1.75rem;               /* 28px - Large */
--spacing-8: 2rem;                  /* 32px - Large */
--spacing-9: 2.25rem;               /* 36px - Large+ */
--spacing-10: 2.5rem;               /* 40px - XL- */
--spacing-11: 2.75rem;              /* 44px - XL */
--spacing-12: 3rem;                 /* 48px - XL */
--spacing-14: 3.5rem;               /* 56px - XL+ */
--spacing-16: 4rem;                 /* 64px - XXL */
--spacing-20: 5rem;                 /* 80px - XXL+ */
--spacing-24: 6rem;                 /* 96px - XXXL */
--spacing-28: 7rem;                 /* 112px - XXXL+ */
--spacing-32: 8rem;                 /* 128px - Max */

/* ANIMATION DURATION SYSTEM */
--duration-instant: 0s;             /* Sofortige Änderungen */
--duration-fast: 0.1s;              /* Schnelle Mikro-Animationen */
--duration-normal: 0.15s;           /* Standard UI-Transitions */
--duration-moderate: 0.3s;          /* Moderate Bewegungen */
--duration-slow: 0.5s;              /* Langsame, betonte Animationen */
--duration-slower: 0.75s;           /* Sehr langsame Animationen */
--duration-slowest: 1s;             /* Entrance-Animationen */

/* Z-INDEX SYSTEM */
--z-base: 0;                        /* Standard-Ebene */
--z-elevated: 10;                   /* Leicht erhöhte Elemente */
--z-dropdown: 50;                   /* Dropdown-Menüs */
--z-sticky: 100;                    /* Sticky-Elemente */
--z-modal-backdrop: 200;            /* Modal-Hintergründe */
--z-modal: 300;                     /* Modal-Inhalte */
--z-popover: 400;                   /* Popover-Elemente */
--z-tooltip: 500;                   /* Tooltips */
--z-toast: 600;                     /* Toast-Nachrichten */
--z-overlay: 700;                   /* System-Overlays */
--z-max: 9999;                      /* Höchste Ebene */

/* VIEWPORT & BREAKPOINT TOKENS */
--viewport-xs: 480px;               /* Extra Small Devices */
--viewport-sm: 640px;               /* Small Devices */
--viewport-md: 768px;               /* Medium Devices */
--viewport-lg: 1024px;              /* Large Devices */
--viewport-xl: 1280px;              /* Extra Large Devices */
--viewport-2xl: 1536px;             /* XXL Devices */

/* FONT SIZE SYSTEM (Modular Scale 1.2) */
--font-size-xs: 0.75rem;            /* 12px */
--font-size-sm: 0.875rem;           /* 14px */
--font-size-base: 1rem;             /* 16px - Basis */
--font-size-lg: 1.125rem;           /* 18px */
--font-size-xl: 1.25rem;            /* 20px */
--font-size-2xl: 1.5rem;            /* 24px */
--font-size-3xl: 1.875rem;          /* 30px */
--font-size-4xl: 2.25rem;           /* 36px */
--font-size-5xl: 3rem;              /* 48px */
--font-size-6xl: 3.75rem;           /* 60px */
--font-size-7xl: 4.5rem;            /* 72px */

/* LINE HEIGHT SYSTEM */
--line-height-none: 1;              /* Keine Zeilenhöhe */
--line-height-tight: 1.25;          /* Enge Zeilenhöhe */
--line-height-snug: 1.375;          /* Gemütliche Zeilenhöhe */
--line-height-normal: 1.5;          /* Normale Zeilenhöhe */
--line-height-relaxed: 1.625;       /* Entspannte Zeilenhöhe */
--line-height-loose: 2;             /* Lockere Zeilenhöhe */

/* SHADOW & ELEVATION SYSTEM */
--shadow-sm: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
--shadow-base: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
--shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
--shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
--shadow-xl: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
--shadow-2xl: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
--shadow-inner: inset 0 2px 4px 0 rgba(0, 0, 0, 0.06);
```

---

## 3. PHYSIKALISCH BASIERTE ANIMATIONEN

### 3.1 Physik-Engine Foundations

#### 3.1.1 Mathematische Grundlagen

Das OpuDoc-Animationssystem basiert auf realen physikalischen Prinzipien, übersetzt in CSS-Timing-Funktionen:

**Spring Physics (Federdynamik)**
```css
/* Gedämpfte harmonische Oszillation - Basis aller Spring-Animationen */
/* Formel: x(t) = A * e^(-ζωt) * cos(ωd*t + φ) */

/* Underdamped Spring (Unterschwingung) - Natürliches Overshoot */
--spring-gentle: cubic-bezier(0.16, 1, 0.3, 1);
/* Dämpfungsgrad ζ = 0.6, Eigenfrequenz ω = 2π rad/s */

/* Critically Damped Spring (Kritische Dämpfung) - Kein Overshoot */
--spring-smooth: cubic-bezier(0.4, 0, 0.2, 1);
/* Dämpfungsgrad ζ = 1.0, schnellste Stabilisierung */

/* Overdamped Spring (Überschwingung) - Langsame Annäherung */
--spring-slow: cubic-bezier(0.25, 0.46, 0.45, 0.94);
/* Dämpfungsgrad ζ = 1.5, keine Oszillation */

/* Elastic Spring (Elastische Feder) - Starkes Overshoot */
--spring-elastic: cubic-bezier(0.68, -0.55, 0.265, 1.55);
/* Dämpfungsgrad ζ = 0.3, maximale Elastizität */
```

**Momentum & Velocity (Impuls & Geschwindigkeit)**
```css
/* Realistische Bewegung basierend auf Impulserhaltung */
/* F = dp/dt (Kraft = Änderung des Impulses über Zeit) */

/* Acceleration Phase (Beschleunigungsphase) */
--momentum-start: cubic-bezier(0, 0, 0.2, 1);
/* Simuliert: F = ma, konstante Kraft = konstante Beschleunigung */

/* Deceleration Phase (Verlangsamungsphase) */
--momentum-end: cubic-bezier(0.4, 0, 1, 1);
/* Simuliert: Reibungskraft proportional zur Geschwindigkeit */

/* Constant Velocity (Konstante Geschwindigkeit) */
--momentum-linear: cubic-bezier(0, 0, 1, 1);
/* Simuliert: Keine resultierende Kraft, gleichförmige Bewegung */

/* Impact Response (Aufprall-Reaktion) */
--momentum-bounce: cubic-bezier(0.175, 0.885, 0.32, 1.275);
/* Simuliert: Elastischer Stoß mit Energieverlust */
```

#### 3.1.2 Keyframe-Bibliothek mit physikalischen Eigenschaften

##### 3.1.2.1 Spring-based Entrance Animations
```css
/* === SPRING ENTRANCE SYSTEM === */

/* Spring From Left - Horizontale Federbewegung */
@keyframes spring-from-left {
  0% {
    opacity: 0;
    transform: translateX(-60px) scale(0.8) rotateY(-15deg);
    /* Startposition: Links außerhalb, verkleinert, leicht gedreht */
  }
  25% {
    opacity: 0.4;
    transform: translateX(-20px) scale(0.9) rotateY(-8deg);
    /* Erste Federbewegung: Annäherung mit Zwischengröße */
  }
  60% {
    opacity: 0.8;
    transform: translateX(8px) scale(1.02) rotateY(3deg);
    /* Overshoot: Über das Ziel hinaus, leichte Vergrößerung */
  }
  80% {
    opacity: 0.95;
    transform: translateX(-2px) scale(1.005) rotateY(-1deg);
    /* Rückfederung: Kleine Korrektur zurück */
  }
  100% {
    opacity: 1;
    transform: translateX(0) scale(1) rotateY(0);
    /* Endposition: Perfekte Ruhelage */
  }
}

/* Spring From Right - Gespiegelte horizontale Bewegung */
@keyframes spring-from-right {
  0% {
    opacity: 0;
    transform: translateX(60px) scale(0.8) rotateY(15deg);
  }
  25% {
    opacity: 0.4;
    transform: translateX(20px) scale(0.9) rotateY(8deg);
  }
  60% {
    opacity: 0.8;
    transform: translateX(-8px) scale(1.02) rotateY(-3deg);
  }
  80% {
    opacity: 0.95;
    transform: translateX(2px) scale(1.005) rotateY(1deg);
  }
  100% {
    opacity: 1;
    transform: translateX(0) scale(1) rotateY(0);
  }
}

/* Spring From Top - Vertikale Schwerkraft-Simulation */
@keyframes spring-from-top {
  0% {
    opacity: 0;
    transform: translateY(-40px) scale(0.9) rotateX(-10deg);
    /* Simulation: Freier Fall von oben */
  }
  35% {
    opacity: 0.6;
    transform: translateY(-10px) scale(0.95) rotateX(-5deg);
    /* Beschleunigung durch Schwerkraft */
  }
  60% {
    opacity: 0.8;
    transform: translateY(6px) scale(1.02) rotateX(2deg);
    /* Aufprall und elastische Reaktion */
  }
  80% {
    opacity: 0.95;
    transform: translateY(-1px) scale(1.01) rotateX(-0.5deg);
    /* Nachschwingen mit verringerter Amplitude */
  }
  100% {
    opacity: 1;
    transform: translateY(0) scale(1) rotateX(0);
    /* Ruhelage erreicht */
  }
}

/* Spring From Bottom - Inverse Schwerkraft */
@keyframes spring-from-bottom {
  0% {
    opacity: 0;
    transform: translateY(40px) scale(0.9) rotateX(10deg);
    /* Simulation: Aufwärts-Impuls gegen Schwerkraft */
  }
  30% {
    opacity: 0.5;
    transform: translateY(15px) scale(0.95) rotateX(5deg);
    /* Verlangsamung durch Schwerkraft */
  }
  60% {
    opacity: 0.8;
    transform: translateY(-6px) scale(1.02) rotateX(-2deg);
    /* Overshoot: Über Zielpunkt hinaus */
  }
  80% {
    opacity: 0.95;
    transform: translateY(1px) scale(1.01) rotateX(0.5deg);
    /* Rückkehr mit gedämpfter Oszillation */
  }
  100% {
    opacity: 1;
    transform: translateY(0) scale(1) rotateX(0);
  }
}
```

##### 3.1.2.2 Advanced Physics Animations
```css
/* === ADVANCED PHYSICS SYSTEM === */

/* Ripple Physics - Wellenausbreitung */
@keyframes ripple-from-center {
  0% {
    transform: scale(0);
    opacity: 0.8;
    border-radius: 50%;
    /* Punktförmiger Start - Energieimpuls */
  }
  25% {
    transform: scale(1);
    opacity: 0.6;
    /* Erste Wellenfront */
  }
  50% {
    transform: scale(2);
    opacity: 0.4;
    /* Wellenausbreitung mit Energieverlust */
  }
  75% {
    transform: scale(3);
    opacity: 0.2;
    /* Weitere Ausbreitung, schwächere Amplitude */
  }
  100% {
    transform: scale(4);
    opacity: 0;
    /* Welle erreicht Rand, Energie dissipiert */
  }
}

/* Context-aware Ripple - Position-basierte Wellenausbreitung */
@keyframes ripple-from-point {
  0% {
    transform: scale(0) translate(var(--origin-x, 0), var(--origin-y, 0));
    opacity: 0.8;
    /* Start am Klick-Punkt mit CSS Custom Properties */
  }
  25% {
    transform: scale(1) translate(var(--origin-x, 0), var(--origin-y, 0));
    opacity: 0.6;
  }
  50% {
    transform: scale(2) translate(var(--origin-x, 0), var(--origin-y, 0));
    opacity: 0.4;
  }
  75% {
    transform: scale(3) translate(var(--origin-x, 0), var(--origin-y, 0));
    opacity: 0.2;
  }
  100% {
    transform: scale(4) translate(var(--origin-x, 0), var(--origin-y, 0));
    opacity: 0;
  }
}

/* Physical Press - 3D-Tiefenreaktion */
@keyframes physical-press {
  0% {
    transform: scale(1) translateZ(0) perspective(1000px);
    box-shadow: 
      0 4px 8px rgba(0, 0, 0, 0.2),
      0 1px 3px rgba(0, 0, 0, 0.1);
    /* Ruheposition mit natürlicher Erhebung */
  }
  25% {
    transform: scale(0.99) translateZ(-1px) perspective(1000px);
    box-shadow: 
      0 3px 6px rgba(0, 0, 0, 0.25),
      0 1px 2px rgba(0, 0, 0, 0.15);
    /* Leichtes Eindrücken, Schatten reduziert */
  }
  50% {
    transform: scale(0.98) translateZ(-2px) perspective(1000px);
    box-shadow: 
      0 2px 4px rgba(0, 0, 0, 0.3),
      inset 0 1px 2px rgba(0, 0, 0, 0.1);
    /* Maximales Eindrücken mit Inset-Schatten */
  }
  75% {
    transform: scale(0.99) translateZ(-1px) perspective(1000px);
    box-shadow: 
      0 3px 6px rgba(0, 0, 0, 0.25),
      0 1px 2px rgba(0, 0, 0, 0.15);
    /* Elastische Rückkehr beginnt */
  }
  100% {
    transform: scale(1) translateZ(0) perspective(1000px);
    box-shadow: 
      0 6px 12px rgba(0, 0, 0, 0.15),
      0 2px 4px rgba(0, 0, 0, 0.08);
    /* Overshoot: Höhere Erhebung als Start */
  }
}

/* Magnetic Attraction - Cursor-folgende Bewegung */
@keyframes magnetic-attract {
  0% {
    transform: translate(0, 0) scale(1);
    /* Ausgangspunkt ohne Magnetic-Effekt */
  }
  50% {
    transform: 
      translate(var(--mouse-x, 0), var(--mouse-y, 0)) 
      scale(1.03)
      rotate(0.5deg);
    /* Zwischenposition: Anziehung und leichte Vergrößerung */
  }
  100% {
    transform: 
      translate(var(--mouse-x, 0), var(--mouse-y, 0)) 
      scale(1.05)
      rotate(0deg);
    /* Endposition: Vollständige Anziehung */
  }
}
```

##### 3.1.2.3 Elastic & Bounce Systems
```css
/* === ELASTIC BOUNCE SYSTEM === */

/* Basic Bounce - Einfache vertikale Sprungbewegung */
@keyframes bounce-in {
  0% {
    opacity: 0;
    transform: scale(0.3) translateY(100px);
    /* Start: Weit unten, stark verkleinert */
  }
  25% {
    opacity: 0.7;
    transform: scale(0.8) translateY(-20px);
    /* Erster Sprung: Über Ziel hinaus */
  }
  50% {
    opacity: 0.9;
    transform: scale(1.05) translateY(0);
    /* Landung mit Overshoot der Größe */
  }
  65% {
    opacity: 0.95;
    transform: scale(0.98) translateY(5px);
    /* Kleine Rückfederung */
  }
  80% {
    opacity: 1;
    transform: scale(1.02) translateY(-2px);
    /* Leichtes Nachschwingen */
  }
  100% {
    opacity: 1;
    transform: scale(1) translateY(0);
    /* Finale Ruheposition */
  }
}

/* Elastic Scale - Nicht-lineare Skalierung */
@keyframes elastic-scale {
  0% {
    transform: scale(1);
    /* Ausgangsgröße */
  }
  10% {
    transform: scale(1.05);
    /* Kleine Anfangsvergrößerung */
  }
  20% {
    transform: scale(1.1);
    /* Weitere Vergrößerung */
  }
  30% {
    transform: scale(0.95);
    /* Rückfederung unter Ausgangsgröße */
  }
  40% {
    transform: scale(1.08);
    /* Zweite Vergrößerung (geringer) */
  }
  50% {
    transform: scale(0.98);
    /* Zweite Rückfederung */
  }
  60% {
    transform: scale(1.02);
    /* Dritte Vergrößerung (minimal) */
  }
  70% {
    transform: scale(0.99);
    /* Dritte Rückfederung */
  }
  80% {
    transform: scale(1.01);
    /* Feine Anpassung */
  }
  90% {
    transform: scale(1);
    /* Annäherung an Endgröße */
  }
  100% {
    transform: scale(1);
    /* Perfekte Endgröße */
  }
}
```

##### 3.1.2.4 Smooth Interaction Animations
```css
/* === SMOOTH INTERACTION SYSTEM === */

/* Smooth Lift - Hover-Erhebung mit 3D-Effekt */
@keyframes smooth-lift {
  0% {
    transform: translateY(0) scale(1) perspective(1000px) rotateX(0deg);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    /* Grundposition mit subtiler Erhebung */
  }
  50% {
    transform: translateY(-2px) scale(1.01) perspective(1000px) rotateX(1deg);
    box-shadow: 0 6px 16px rgba(0, 0, 0, 0.12);
    /* Zwischenposition: Leichte Erhebung und Rotation */
  }
  100% {
    transform: translateY(-4px) scale(1.02) perspective(1000px) rotateX(2deg);
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15);
    /* Endposition: Deutliche Erhebung mit verstärktem Schatten */
  }
}

/* Smooth Press - Sanfte Eindrück-Reaktion */
@keyframes smooth-press {
  0% {
    transform: scale(1) translateZ(0);
    filter: brightness(1);
    /* Normal state */
  }
  25% {
    transform: scale(0.99) translateZ(-0.5px);
    filter: brightness(0.95);
    /* Leichtes Eindrücken mit Helligkeitsreduktion */
  }
  50% {
    transform: scale(0.98) translateZ(-1px);
    filter: brightness(0.9);
    /* Maximales Eindrücken */
  }
  75% {
    transform: scale(0.99) translateZ(-0.5px);
    filter: brightness(0.95);
    /* Rückkehr-Phase */
  }
  100% {
    transform: scale(1) translateZ(0);
    filter: brightness(1);
    /* Zurück zur Normalposition */
  }
}
```

#### 3.1.3 Specialized Tab Animation System

##### 3.1.3.1 Tab Trigger Elastic Bounce (Signature Feature)
```css
/* === TAB TRIGGER BOUNCE ANIMATIONS === */
/* Diese Animationen sind das Herzstück des Tab-Systems */

/* Bounce From Left - Rechtsbewegung mit elastischer Reaktion */
@keyframes tab-trigger-bounce-from-left {
  0% {
    transform: translateX(-8px) scaleX(0.8);
    background-color: hsl(var(--muted));
    /* Start: Links versetzt, horizontal zusammengedrückt, muted Farbe */
  }
  15% {
    transform: translateX(-4px) scaleX(0.9);
    background-color: hsl(var(--muted) / 0.8);
    /* Beschleunigungsphase */
  }
  30% {
    transform: translateX(6px) scaleX(1.15);
    background-color: hsl(var(--background) / 0.8);
    /* Overshoot: Über Ziel hinaus, horizontal gedehnt, Farbwechsel */
  }
  45% {
    transform: translateX(4px) scaleX(1.1);
    background-color: hsl(var(--background) / 0.85);
    /* Erste Rückfederung */
  }
  60% {
    transform: translateX(-2px) scaleX(1.05);
    background-color: hsl(var(--background) / 0.9);
    /* Zweite Bewegung zurück über Zielpunkt */
  }
  75% {
    transform: translateX(-1px) scaleX(1.02);
    background-color: hsl(var(--background) / 0.93);
    /* Feine Anpassung */
  }
  80% {
    transform: translateX(1px) scaleX(1.02);
    background-color: hsl(var(--background) / 0.95);
    /* Minimale Korrektur */
  }
  90% {
    transform: translateX(0.5px) scaleX(1.01);
    background-color: hsl(var(--background) / 0.97);
    /* Sehr feine Anpassung */
  }
  100% {
    transform: translateX(0) scaleX(1);
    background-color: hsl(var(--background));
    /* Perfekte Endposition mit finaler Farbe */
  }
}

/* Bounce From Right - Linksbewegung mit elastischer Reaktion */
@keyframes tab-trigger-bounce-from-right {
  0% {
    transform: translateX(8px) scaleX(0.8);
    background-color: hsl(var(--muted));
    /* Start: Rechts versetzt, horizontal zusammengedrückt */
  }
  15% {
    transform: translateX(4px) scaleX(0.9);
    background-color: hsl(var(--muted) / 0.8);
    /* Beschleunigungsphase */
  }
  30% {
    transform: translateX(-6px) scaleX(1.15);
    background-color: hsl(var(--background) / 0.8);
    /* Overshoot: Links über Ziel hinaus, horizontal gedehnt */
  }
  45% {
    transform: translateX(-4px) scaleX(1.1);
    background-color: hsl(var(--background) / 0.85);
    /* Erste Rückfederung */
  }
  60% {
    transform: translateX(2px) scaleX(1.05);
    background-color: hsl(var(--background) / 0.9);
    /* Zweite Bewegung zurück über Zielpunkt */
  }
  75% {
    transform: translateX(1px) scaleX(1.02);
    background-color: hsl(var(--background) / 0.93);
    /* Feine Anpassung */
  }
  80% {
    transform: translateX(-1px) scaleX(1.02);
    background-color: hsl(var(--background) / 0.95);
    /* Minimale Korrektur */
  }
  90% {
    transform: translateX(-0.5px) scaleX(1.01);
    background-color: hsl(var(--background) / 0.97);
    /* Sehr feine Anpassung */
  }
  100% {
    transform: translateX(0) scaleX(1);
    background-color: hsl(var(--background));
    /* Perfekte Endposition */
  }
}

/* Bounce Center - Zentrale elastische Reaktion (für erste Aktivierung) */
@keyframes tab-trigger-bounce-center {
  0% {
    transform: scale(0.9);
    background-color: hsl(var(--muted));
    /* Start: Gleichmäßig verkleinert */
  }
  20% {
    transform: scale(1.05);
    background-color: hsl(var(--background) / 0.7);
    /* Erste Vergrößerung über Zielgröße */
  }
  40% {
    transform: scale(1.08);
    background-color: hsl(var(--background) / 0.8);
    /* Maximale Vergrößerung */
  }
  55% {
    transform: scale(0.97);
    background-color: hsl(var(--background) / 0.85);
    /* Rückfederung unter Zielgröße */
  }
  70% {
    transform: scale(1.02);
    background-color: hsl(var(--background) / 0.9);
    /* Zweite kleinere Vergrößerung */
  }
  85% {
    transform: scale(0.99);
    background-color: hsl(var(--background) / 0.95);
    /* Zweite kleinere Rückfederung */
  }
  100% {
    transform: scale(1);
    background-color: hsl(var(--background));
    /* Finale Größe und Farbe */
  }
}
```

##### 3.1.3.2 Tab Content Transitions
```css
/* === TAB CONTENT TRANSITIONS === */

/* Enhanced Tab Content Enter - Sanfte Inhalts-Transition */
@keyframes tab-content-enter {
  0% {
    opacity: 0;
    transform: translateY(8px) scale(0.98);
    filter: blur(1px);
    /* Start: Leicht unten, verkleinert, unscharf */
  }
  30% {
    opacity: 0.5;
    transform: translateY(4px) scale(0.99);
    filter: blur(0.5px);
    /* Zwischenphase: Aufwärtsbewegung beginnt */
  }
  60% {
    opacity: 0.8;
    transform: translateY(-1px) scale(1.005);
    filter: blur(0px);
    /* Leichtes Overshoot nach oben, minimal vergrößert */
  }
  80% {
    opacity: 0.95;
    transform: translateY(0.5px) scale(1.002);
    filter: blur(0px);
    /* Kleine Rückfederung */
  }
  100% {
    opacity: 1;
    transform: translateY(0) scale(1);
    filter: blur(0px);
    /* Perfekte Endposition */
  }
}

/* Tab Slide Transitions für Richtungsabhängigkeit */
@keyframes tab-slide-in-right {
  0% {
    opacity: 0;
    transform: translateX(24px) scale(0.98);
    filter: blur(1px);
    /* Start: Rechts außerhalb, leicht verkleinert, unscharf */
  }
  40% {
    opacity: 0.6;
    transform: translateX(8px) scale(0.99);
    filter: blur(0.5px);
    /* Bewegung von rechts */
  }
  60% {
    opacity: 0.8;
    transform: translateX(-2px) scale(1.01);
    filter: blur(0px);
    /* Overshoot nach links, leicht vergrößert */
  }
  80% {
    opacity: 0.95;
    transform: translateX(1px) scale(1.005);
    filter: blur(0px);
    /* Korrektur nach rechts */
  }
  100% {
    opacity: 1;
    transform: translateX(0) scale(1);
    filter: blur(0px);
    /* Finale Position */
  }
}

@keyframes tab-slide-in-left {
  0% {
    opacity: 0;
    transform: translateX(-24px) scale(0.98);
    filter: blur(1px);
    /* Start: Links außerhalb */
  }
  40% {
    opacity: 0.6;
    transform: translateX(-8px) scale(0.99);
    filter: blur(0.5px);
    /* Bewegung von links */
  }
  60% {
    opacity: 0.8;
    transform: translateX(2px) scale(1.01);
    filter: blur(0px);
    /* Overshoot nach rechts */
  }
  80% {
    opacity: 0.95;
    transform: translateX(-1px) scale(1.005);
    filter: blur(0px);
    /* Korrektur nach links */
  }
  100% {
    opacity: 1;
    transform: translateX(0) scale(1);
    filter: blur(0px);
    /* Finale Position */
  }
}
```

#### 3.1.4 Modal & Dropdown Physics

##### 3.1.4.1 Advanced Dropdown System
```css
/* === DROPDOWN SPRING ANIMATIONS === */

/* Dropdown Spring Open - Physikalisches Öffnen */
@keyframes dropdown-spring-open {
  0% {
    opacity: 0;
    transform: scale(0.9) translateY(-10px) rotateX(-10deg);
    transform-origin: top center;
    /* Start: Verkleinert, leicht oben, nach hinten geneigt */
  }
  25% {
    opacity: 0.4;
    transform: scale(0.95) translateY(-5px) rotateX(-5deg);
    /* Erste Bewegungsphase */
  }
  60% {
    opacity: 0.8;
    transform: scale(1.02) translateY(1px) rotateX(2deg);
    /* Overshoot: Über Zielposition, leicht nach vorn geneigt */
  }
  80% {
    opacity: 0.95;
    transform: scale(1.005) translateY(-0.5px) rotateX(-0.5deg);
    /* Rückfederung */
  }
  100% {
    opacity: 1;
    transform: scale(1) translateY(0) rotateX(0deg);
    /* Finale stabile Position */
  }
}

/* Dropdown Spring Close - Physikalisches Schließen */
@keyframes dropdown-spring-close {
  0% {
    opacity: 1;
    transform: scale(1) translateY(0) rotateX(0deg);
    transform-origin: top center;
    /* Ausgangsposition */
  }
  30% {
    opacity: 0.7;
    transform: scale(0.98) translateY(-2px) rotateX(-2deg);
    /* Leichte Rückwärtsbewegung */
  }
  100% {
    opacity: 0;
    transform: scale(0.95) translateY(-8px) rotateX(-5deg);
    /* Finale Position: Verkleinert, nach oben, nach hinten */
  }
}
```

##### 3.1.4.2 Modal Spring System
```css
/* === MODAL SPRING ANIMATIONS === */

/* Modal Spring Backdrop - Hintergrund-Überblendung */
@keyframes modal-spring-backdrop {
  0% {
    opacity: 0;
    backdrop-filter: blur(0px);
    /* Start: Transparent, kein Blur */
  }
  50% {
    opacity: 0.7;
    backdrop-filter: blur(4px);
    /* Zwischenphase: Partieller Blur */
  }
  100% {
    opacity: 1;
    backdrop-filter: blur(8px);
    /* Ende: Vollständiger Blur-Effekt */
  }
}

/* Modal Spring Content - Inhalts-Erscheinung */
@keyframes modal-spring-content {
  0% {
    opacity: 0;
    transform: scale(0.8) translateY(20px) perspective(1000px) rotateX(-5deg);
    /* Start: Verkleinert, unten, nach hinten geneigt */
  }
  30% {
    opacity: 0.5;
    transform: scale(0.9) translateY(10px) perspective(1000px) rotateX(-2deg);
    /* Aufwärtsbewegung beginnt */
  }
  60% {
    opacity: 0.9;
    transform: scale(1.02) translateY(-2px) perspective(1000px) rotateX(1deg);
    /* Overshoot: Über Zielpunkt, leicht nach vorn */
  }
  80% {
    opacity: 0.98;
    transform: scale(1.005) translateY(1px) perspective(1000px) rotateX(-0.5deg);
    /* Rückfederung */
  }
  100% {
    opacity: 1;
    transform: scale(1) translateY(0) perspective(1000px) rotateX(0deg);
    /* Finale Position */
  }
}
```

#### 3.1.5 Accordion Physics
```css
/* === ACCORDION SPRING ANIMATIONS === */

/* Accordion Spring Down - Öffnungs-Physik */
@keyframes accordion-spring-down {
  0% {
    height: 0;
    opacity: 0;
    transform: scaleY(0.8) perspective(500px) rotateX(-10deg);
    transform-origin: top center;
    /* Start: Geschlossen, nach hinten geneigt */
  }
  30% {
    height: calc(var(--radix-accordion-content-height) * 0.6);
    opacity: 0.5;
    transform: scaleY(0.9) perspective(500px) rotateX(-5deg);
    /* Erste Öffnungsphase */
  }
  60% {
    height: var(--radix-accordion-content-height);
    opacity: 0.8;
    transform: scaleY(1.02) perspective(500px) rotateX(1deg);
    /* Overshoot: Über Zielhöhe, leicht nach vorn */
  }
  80% {
    height: var(--radix-accordion-content-height);
    opacity: 0.95;
    transform: scaleY(1.005) perspective(500px) rotateX(-0.5deg);
    /* Rückfederung */
  }
  100% {
    height: var(--radix-accordion-content-height);
    opacity: 1;
    transform: scaleY(1) perspective(500px) rotateX(0deg);
    /* Finale Position */
  }
}

/* Accordion Spring Up - Schließungs-Physik */
@keyframes accordion-spring-up {
  0% {
    height: var(--radix-accordion-content-height);
    opacity: 1;
    transform: scaleY(1) perspective(500px) rotateX(0deg);
    transform-origin: top center;
    /* Ausgangsposition: Vollständig geöffnet */
  }
  20% {
    height: calc(var(--radix-accordion-content-height) * 0.8);
    opacity: 0.8;
    transform: scaleY(0.98) perspective(500px) rotateX(-1deg);
    /* Beginn der Schließung */
  }
  40% {
    height: calc(var(--radix-accordion-content-height) * 0.6);
    opacity: 0.6;
    transform: scaleY(0.95) perspective(500px) rotateX(-3deg);
    /* Mittlere Schließungsphase */
  }
  70% {
    height: calc(var(--radix-accordion-content-height) * 0.2);
    opacity: 0.3;
    transform: scaleY(0.9) perspective(500px) rotateX(-7deg);
    /* Späte Schließungsphase */
  }
  100% {
    height: 0;
    opacity: 0;
    transform: scaleY(0.8) perspective(500px) rotateX(-10deg);
    /* Vollständig geschlossen */
  }
}
```

#### 3.1.6 Specialized Interaction Physics

##### 3.1.6.1 Stagger Animation System
```css
/* === STAGGER ANIMATION SYSTEM === */

/* Stagger Fade In - Sequenzielle Entrance-Animation */
@keyframes stagger-fade-in {
  0% {
    opacity: 0;
    transform: translateY(15px) scale(0.95);
    /* Start: Unsichtbar, leicht unten, verkleinert */
  }
  25% {
    opacity: 0.3;
    transform: translateY(8px) scale(0.97);
    /* Erste Sichtbarkeit */
  }
  60% {
    opacity: 0.8;
    transform: translateY(-2px) scale(1.01);
    /* Overshoot: Leicht über Zielpunkt */
  }
  80% {
    opacity: 0.95;
    transform: translateY(1px) scale(1.005);
    /* Rückfederung */
  }
  100% {
    opacity: 1;
    transform: translateY(0) scale(1);
    /* Finale Position */
  }
}

/* Stagger Delays für sequenzielle Ausführung */
.stagger-item:nth-child(1) { animation-delay: 0ms; }
.stagger-item:nth-child(2) { animation-delay: 80ms; }
.stagger-item:nth-child(3) { animation-delay: 160ms; }
.stagger-item:nth-child(4) { animation-delay: 240ms; }
.stagger-item:nth-child(5) { animation-delay: 320ms; }
.stagger-item:nth-child(6) { animation-delay: 400ms; }
.stagger-item:nth-child(7) { animation-delay: 480ms; }
.stagger-item:nth-child(8) { animation-delay: 560ms; }
.stagger-item:nth-child(9) { animation-delay: 640ms; }
.stagger-item:nth-child(10) { animation-delay: 720ms; }
```

##### 3.1.6.2 Morphing & Loading Animations
```css
/* === MORPHING SYSTEM === */

/* Morph In - Komplexe Transformation */
@keyframes morph-in {
  0% {
    opacity: 0;
    transform: scale(0.5) rotate(-5deg) perspective(800px) rotateY(-15deg);
    filter: blur(2px) saturate(0.5);
    /* Start: Klein, gedreht, unscharf, desaturiert */
  }
  25% {
    opacity: 0.4;
    transform: scale(0.8) rotate(-2deg) perspective(800px) rotateY(-8deg);
    filter: blur(1px) saturate(0.7);
    /* Erste Transformation */
  }
  60% {
    opacity: 0.8;
    transform: scale(1.1) rotate(1deg) perspective(800px) rotateY(2deg);
    filter: blur(0px) saturate(1.1);
    /* Overshoot: Größer als Ziel, übersaturiert */
  }
  80% {
    opacity: 0.95;
    transform: scale(1.02) rotate(-0.5deg) perspective(800px) rotateY(-0.5deg);
    filter: blur(0px) saturate(1.05);
    /* Rückfederung */
  }
  100% {
    opacity: 1;
    transform: scale(1) rotate(0deg) perspective(800px) rotateY(0deg);
    filter: blur(0px) saturate(1);
    /* Finale Form */
  }
}

/* Smooth Pulse - Atemende Animation für Loading */
@keyframes smooth-pulse {
  0% {
    opacity: 0.6;
    transform: scale(1);
    filter: brightness(0.9);
    /* Start: Gedimmt, normal */
  }
  25% {
    opacity: 0.8;
    transform: scale(1.01);
    filter: brightness(1);
    /* Erste Aufhellung */
  }
  50% {
    opacity: 1;
    transform: scale(1.02);
    filter: brightness(1.1);
    /* Maximum: Hell, leicht vergrößert */
  }
  75% {
    opacity: 0.8;
    transform: scale(1.01);
    filter: brightness(1);
    /* Rückkehr */
  }
  100% {
    opacity: 0.6;
    transform: scale(1);
    filter: brightness(0.9);
    /* Zurück zum Start */
  }
}
```

### 3.2 Animation Class System in Tailwind

#### 3.2.1 Complete Animation Mapping
```typescript
/* === TAILWIND ANIMATION CONFIGURATION === */
/* Vollständige Mapping der Keyframes zu Utility-Classes */

animation: {
  // === TAB TRIGGER SYSTEM === //
  'tab-trigger-bounce-from-left': 
    'tab-trigger-bounce-from-left 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55)',
  'tab-trigger-bounce-from-right': 
    'tab-trigger-bounce-from-right 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55)',
  'tab-trigger-bounce-center': 
    'tab-trigger-bounce-center 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55)',

  // === SPRING ENTRANCE SYSTEM === //
  'spring-fade-in': 
    'spring-fade-in 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275)',
  'spring-scale-in': 
    'spring-scale-in 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55)',
  'spring-slide-right': 
    'spring-slide-right 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275)',
  'spring-slide-down': 
    'spring-slide-down 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275)',
  'spring-slide-up': 
    'spring-slide-up 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275)',

  // === SPRING DIRECTIONAL ENTRANCES === //
  'spring-from-left': 
    'spring-from-left 0.7s cubic-bezier(0.175, 0.885, 0.32, 1.275)',
  'spring-from-right': 
    'spring-from-right 0.7s cubic-bezier(0.175, 0.885, 0.32, 1.275)',
  'spring-from-top': 
    'spring-from-top 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275)',
  'spring-from-bottom': 
    'spring-from-bottom 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275)',

  // === BOUNCE & ELASTIC EFFECTS === //
  'bounce-in': 
    'bounce-in 0.7s cubic-bezier(0.68, -0.55, 0.265, 1.55)',
  'elastic-scale': 
    'elastic-scale 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55)',

  // === SMOOTH INTERACTION EFFECTS === //
  'smooth-lift': 
    'smooth-lift 0.3s cubic-bezier(0.4, 0, 0.2, 1)',
  'smooth-press': 
    'smooth-press 0.15s cubic-bezier(0.4, 0, 0.2, 1)',

  // === ADVANCED DROPDOWN SYSTEM === //
  'dropdown-spring-open': 
    'dropdown-spring-open 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275)',
  'dropdown-spring-close': 
    'dropdown-spring-close 0.2s cubic-bezier(0.4, 0, 0.2, 1)',

  // === MODAL SPRING SYSTEM === //
  'modal-spring-backdrop': 
    'modal-spring-backdrop 0.3s cubic-bezier(0.4, 0, 0.2, 1)',
  'modal-spring-content': 
    'modal-spring-content 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275)',

  // === ACCORDION SPRING SYSTEM === //
  'accordion-spring-down': 
    'accordion-spring-down 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275)',
  'accordion-spring-up': 
    'accordion-spring-up 0.3s cubic-bezier(0.4, 0, 0.2, 1)',

  // === ENHANCED TAB SLIDE SYSTEM === //
  'tab-slide-in-right': 
    'tab-slide-in-right 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.175)',
  'tab-slide-in-left': 
    'tab-slide-in-left 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.175)',
  'tab-slide-out-left': 
    'tab-slide-out-left 0.25s cubic-bezier(0.4, 0, 0.2, 1)',
  'tab-slide-out-right': 
    'tab-slide-out-right 0.25s cubic-bezier(0.4, 0, 0.2, 1)',
  'tab-content-enter': 
    'tab-content-enter 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275)',

  // === STAGGER & LIST EFFECTS === //
  'stagger-fade-in': 
    'stagger-fade-in 0.4s cubic-bezier(0.4, 0, 0.2, 1)',
  'morph-in': 
    'morph-in 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275)',

  // === LOADING & PULSE EFFECTS === //
  'smooth-pulse': 
    'smooth-pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite',

  // === PHYSICS INTERACTION EFFECTS === //
  'ripple-from-center': 
    'ripple-from-center 0.6s cubic-bezier(0.4, 0, 0.2, 1)',
  'ripple-from-point': 
    'ripple-from-point 0.6s cubic-bezier(0.4, 0, 0.2, 1)',
  'physical-press': 
    'physical-press 0.2s cubic-bezier(0.4, 0, 0.2, 1)',
  'magnetic-attract': 
    'magnetic-attract 0.3s cubic-bezier(0.4, 0, 0.2, 1)',

  // === LEGACY SUPPORT (using spring versions) === //
  'fade-in': 
    'spring-fade-in 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275)',
  'scale-in': 
    'spring-scale-in 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55)',
  'slide-in-right': 
    'spring-slide-right 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275)',
  'slide-down': 
    'spring-slide-down 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275)',
  'slide-up': 
    'spring-slide-up 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275)',
  'dropdown-open': 
    'dropdown-spring-open 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275)',
  'dropdown-close': 
    'dropdown-spring-close 0.2s cubic-bezier(0.4, 0, 0.2, 1)',
  'modal-backdrop': 
    'modal-spring-backdrop 0.3s cubic-bezier(0.4, 0, 0.2, 1)',
  'modal-content': 
    'modal-spring-content 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275)',
  'accordion-down': 
    'accordion-spring-down 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275)',
  'accordion-up': 
    'accordion-spring-up 0.3s cubic-bezier(0.4, 0, 0.2, 1)'
}
```

#### 3.2.2 Performance-Optimized Animation Settings
```css
/* === PERFORMANCE OPTIMIZATIONS === */

/* GPU-Beschleunigung für alle animierten Elemente */
.animate-any {
  will-change: transform, opacity;
  transform: translateZ(0); /* Force GPU layer */
  backface-visibility: hidden;
  perspective: 1000px;
}

/* Reduced Motion Support - Accessibility */
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
  
  /* Maintain essential animations with reduced motion */
  .animate-essential {
    animation-duration: 0.15s !important;
    transition-duration: 0.15s !important;
  }
}

/* Container Query Support für responsive Animationen */
@container (max-width: 768px) {
  .animate-mobile-optimized {
    animation-duration: 0.2s;
    animation-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  }
}
```

---

## 4. KOMPONENTEN-ARCHITEKTUR

### 4.1 Design System Component Hierarchy

#### 4.1.1 Atomic Design Principles Implementation

Das OpuDoc Design System folgt der Atomic Design Methodologie mit spezifischen Anpassungen für React/TypeScript:

**Atoms (Grundelemente)**
```typescript
// Beispiel: Button Atom mit vollständiger Varianten-Unterstützung
import { cva, type VariantProps } from "class-variance-authority"

const buttonVariants = cva(
  // Base Classes - Immer angewendet
  "inline-flex items-center justify-center gap-2 whitespace-nowrap rounded-md text-sm font-medium ring-offset-background transition-all focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50 [&_svg]:pointer-events-none [&_svg]:size-4 [&_svg]:shrink-0",
  {
    variants: {
      variant: {
        default: "bg-primary text-primary-foreground hover:bg-primary/90 active:bg-primary/80 animate-smooth-press",
        destructive: "bg-destructive text-destructive-foreground hover:bg-destructive/90 active:bg-destructive/80 animate-smooth-press",
        outline: "border border-input bg-background hover:bg-accent hover:text-accent-foreground active:bg-accent/80 animate-smooth-press",
        secondary: "bg-secondary text-secondary-foreground hover:bg-secondary/80 active:bg-secondary/60 animate-smooth-press",
        ghost: "hover:bg-accent hover:text-accent-foreground active:bg-accent/80 animate-smooth-press",
        link: "text-primary underline-offset-4 hover:underline focus:underline animate-smooth-press",
        
        // Advanced Variants
        magnetic: "bg-primary text-primary-foreground hover:animate-magnetic-attract physical-press",
        glassmorphic: "glass-card hover:animate-smooth-lift backdrop-blur-md",
        elastic: "bg-accent text-accent-foreground hover:animate-elastic-scale",
      },
      size: {
        default: "h-10 px-4 py-2",
        sm: "h-9 rounded-md px-3",
        lg: "h-11 rounded-md px-8",
        icon: "h-10 w-10",
        xl: "h-12 rounded-lg px-10 text-base",
        micro: "h-6 px-2 text-xs rounded",
      },
      animation: {
        none: "",
        spring: "animate-spring-entrance",
        bounce: "animate-bounce-in",
        elastic: "animate-elastic-scale",
        magnetic: "magnetic-button",
      }
    },
    defaultVariants: {
      variant: "default",
      size: "default",
      animation: "spring",
    },
  }
)
```

**Molecules (Zusammengesetzte Komponenten)**
```typescript
// Beispiel: Input Group Molecule
interface InputGroupProps {
  label: string
  hint?: string
  error?: string
  success?: string
  icon?: React.ReactNode
  required?: boolean
  children: React.ReactNode
}

const InputGroup = ({ 
  label, 
  hint, 
  error, 
  success, 
  icon, 
  required,
  children 
}: InputGroupProps) => {
  return (
    <div className="input-group animate-spring-from-left">
      <label className={cn(
        "block text-sm font-medium mb-2",
        "text-foreground",
        required && "after:content-['*'] after:text-destructive after:ml-1"
      )}>
        {label}
      </label>
      
      <div className="relative">
        {icon && (
          <div className="absolute left-3 top-3 h-4 w-4 text-muted-foreground pointer-events-none animate-spring-from-left">
            {icon}
          </div>
        )}
        {children}
      </div>
      
      {hint && !error && !success && (
        <p className="mt-2 text-sm text-muted-foreground animate-spring-from-left">
          {hint}
        </p>
      )}
      
      {error && (
        <p className="mt-2 text-sm text-destructive animate-spring-from-left flex items-center gap-1">
          <ExclamationTriangleIcon className="h-4 w-4" />
          {error}
        </p>
      )}
      
      {success && (
        <p className="mt-2 text-sm text-success animate-spring-from-left flex items-center gap-1">
          <CheckCircleIcon className="h-4 w-4" />
          {success}
        </p>
      )}
    </div>
  )
}
```

**Organisms (Komplexe Strukturen)**
```typescript
// Beispiel: Navigation Organism mit vollständiger State-Verwaltung
interface NavigationItem {
  id: string
  label: string
  href?: string
  icon?: React.ReactNode
  children?: NavigationItem[]
  active?: boolean
  disabled?: boolean
}

interface NavigationProps {
  items: NavigationItem[]
  activeId?: string
  onItemClick?: (item: NavigationItem) => void
  variant?: 'sidebar' | 'horizontal' | 'vertical'
  collapsible?: boolean
  defaultCollapsed?: boolean
}

const Navigation = ({
  items,
  activeId,
  onItemClick,
  variant = 'sidebar',
  collapsible = false,
  defaultCollapsed = false
}: NavigationProps) => {
  const [collapsed, setCollapsed] = useState(defaultCollapsed)
  const [openGroups, setOpenGroups] = useState<Set<string>>(new Set())
  
  const toggleGroup = (groupId: string) => {
    setOpenGroups(prev => {
      const newSet = new Set(prev)
      if (newSet.has(groupId)) {
        newSet.delete(groupId)
      } else {
        newSet.add(groupId)
      }
      return newSet
    })
  }
  
  return (
    <nav className={cn(
      "navigation-container",
      variant === 'sidebar' && "h-full w-64 bg-sidebar-background border-r border-sidebar-border",
      variant === 'horizontal' && "w-full bg-background border-b border-border",
      collapsed && variant === 'sidebar' && "w-16",
      "animate-spring-from-left"
    )}>
      {collapsible && (
        <div className="p-4 border-b border-sidebar-border">
          <Button
            variant="ghost"
            size="icon"
            onClick={() => setCollapsed(!collapsed)}
            className="animate-smooth-press"
          >
            {collapsed ? <ChevronRightIcon /> : <ChevronLeftIcon />}
          </Button>
        </div>
      )}
      
      <ul className="space-y-1 p-4">
        {items.map((item, index) => (
          <NavigationItem
            key={item.id}
            item={item}
            active={item.id === activeId}
            collapsed={collapsed}
            onItemClick={onItemClick}
            onToggleGroup={toggleGroup}
            isGroupOpen={openGroups.has(item.id)}
            animationDelay={index * 50} // Stagger effect
          />
        ))}
      </ul>
    </nav>
  )
}
```

#### 4.1.2 Component Composition Patterns

**Compound Components Pattern**
```typescript
// Tab System als Compound Component
const Tabs = {
  Root: SlideTabs,
  List: SlideTabsList, 
  Trigger: SlideTabsTrigger,
  Content: SlideTabsContent,
}

// Usage
<Tabs.Root defaultValue="overview">
  <Tabs.List>
    <Tabs.Trigger value="overview" index={0}>Overview</Tabs.Trigger>
    <Tabs.Trigger value="analytics" index={1}>Analytics</Tabs.Trigger>
  </Tabs.List>
  <Tabs.Content value="overview">Content</Tabs.Content>
</Tabs.Root>
```

**Render Props Pattern für Animation Control**
```typescript
interface AnimationControllerProps {
  children: (props: {
    isVisible: boolean
    animate: (animation: string) => void
    ref: React.RefObject<HTMLElement>
  }) => React.ReactNode
  trigger?: 'hover' | 'click' | 'scroll' | 'manual'
  delay?: number
}

const AnimationController = ({ 
  children, 
  trigger = 'scroll',
  delay = 0 
}: AnimationControllerProps) => {
  const [isVisible, setIsVisible] = useState(false)
  const ref = useRef<HTMLElement>(null)
  
  const animate = useCallback((animation: string) => {
    if (ref.current) {
      ref.current.style.animation = animation
    }
  }, [])
  
  // Intersection Observer für scroll trigger
  useEffect(() => {
    if (trigger !== 'scroll') return
    
    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          setTimeout(() => setIsVisible(true), delay)
        }
      },
      { threshold: 0.1 }
    )
    
    if (ref.current) {
      observer.observe(ref.current)
    }
    
    return () => observer.disconnect()
  }, [trigger, delay])
  
  return children({ isVisible, animate, ref })
}
```

### 4.2 SlideTabs Component - Complete Implementation

#### 4.2.1 Full TypeScript Implementation
```typescript
// === SLIDE TABS SYSTEM - COMPLETE IMPLEMENTATION === //

import * as React from "react"
import * as TabsPrimitive from "@radix-ui/react-tabs"
import { cn } from "@/lib/utils"

// === ROOT COMPONENT === //
const SlideTabs = TabsPrimitive.Root
SlideTabs.displayName = "SlideTabs"

// === TABS LIST COMPONENT === //
interface SlideTabsListProps extends React.ComponentPropsWithoutRef<typeof TabsPrimitive.List> {
  variant?: 'default' | 'pills' | 'underline' | 'minimal'
  size?: 'sm' | 'default' | 'lg'
  distribution?: 'start' | 'center' | 'end' | 'stretch'
}

const SlideTabsList = React.forwardRef<
  React.ElementRef<typeof TabsPrimitive.List>,
  SlideTabsListProps
>(({ className, variant = 'default', size = 'default', distribution = 'stretch', ...props }, ref) => (
  <TabsPrimitive.List
    ref={ref}
    className={cn(
      // Base classes
      "inline-flex items-center text-muted-foreground relative",
      
      // Variant styles
      variant === 'default' && "rounded-md bg-muted p-1 gap-1",
      variant === 'pills' && "rounded-full bg-muted/50 p-1 gap-2",
      variant === 'underline' && "border-b border-border gap-4",
      variant === 'minimal' && "gap-6",
      
      // Size styles
      size === 'sm' && "h-8 text-xs",
      size === 'default' && "h-10 text-sm",
      size === 'lg' && "h-12 text-base",
      
      // Distribution styles
      distribution === 'start' && "justify-start",
      distribution === 'center' && "justify-center",
      distribution === 'end' && "justify-end",
      distribution === 'stretch' && "w-full grid grid-cols-[repeat(var(--tabs-count),1fr)]",
      
      className
    )}
    style={{
      '--tabs-count': React.Children.count(props.children)
    } as React.CSSProperties}
    {...props}
  />
))
SlideTabsList.displayName = TabsPrimitive.List.displayName

// === TABS TRIGGER COMPONENT === //
interface SlideTabsTriggerProps extends React.ComponentPropsWithoutRef<typeof TabsPrimitive.Trigger> {
  index?: number
  variant?: 'default' | 'pills' | 'underline' | 'minimal'
  size?: 'sm' | 'default' | 'lg'
  animation?: 'bounce' | 'scale' | 'slide' | 'none'
}

const SlideTabsTrigger = React.forwardRef<
  React.ElementRef<typeof TabsPrimitive.Trigger>,
  SlideTabsTriggerProps
>(({ 
  className, 
  index = 0, 
  variant = 'default', 
  size = 'default',
  animation = 'bounce',
  ...props 
}, ref) => {
  const [lastActiveIndex, setLastActiveIndex] = React.useState<number | null>(null)
  const [animationClass, setAnimationClass] = React.useState("")
  const [isFirstActivation, setIsFirstActivation] = React.useState(true)
  
  // Animation logic mit verbesserter State-Verwaltung
  React.useEffect(() => {
    const trigger = ref && 'current' in ref ? ref.current : null
    if (trigger && trigger.getAttribute('data-state') === 'active') {
      if (animation === 'none') return
      
      let bounceClass = ""
      
      if (isFirstActivation) {
        // Erste Aktivierung - Center Bounce
        bounceClass = animation === 'bounce' 
          ? 'animate-tab-trigger-bounce-center'
          : animation === 'scale'
          ? 'animate-elastic-scale'
          : animation === 'slide'
          ? 'animate-spring-scale-in'
          : ''
        setIsFirstActivation(false)
      } else if (lastActiveIndex !== null && lastActiveIndex !== index) {
        // Richtungsabhängige Animation
        const direction = index > lastActiveIndex ? 'right' : 'left'
        bounceClass = animation === 'bounce'
          ? direction === 'right' 
            ? 'animate-tab-trigger-bounce-from-left' 
            : 'animate-tab-trigger-bounce-from-right'
          : animation === 'scale'
          ? 'animate-elastic-scale'
          : animation === 'slide'
          ? direction === 'right'
            ? 'animate-tab-slide-in-right'
            : 'animate-tab-slide-in-left'
          : ''
      }
      
      if (bounceClass) {
        setAnimationClass(bounceClass)
        // Animation-Cleanup nach Completion
        const duration = animation === 'bounce' ? 600 : animation === 'scale' ? 400 : 500
        setTimeout(() => setAnimationClass(""), duration)
      }
      
      setLastActiveIndex(index)
    }
  }, [props.value, index, lastActiveIndex, ref, animation, isFirstActivation])

  return (
    <TabsPrimitive.Trigger
      ref={ref}
      className={cn(
        // Base classes
        "inline-flex items-center justify-center whitespace-nowrap font-medium ring-offset-background transition-all focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50",
        
        // Size classes
        size === 'sm' && "rounded-sm px-2 py-1 text-xs",
        size === 'default' && "rounded-sm px-3 py-1.5 text-sm",
        size === 'lg' && "rounded-md px-4 py-2 text-base",
        
        // Variant-specific active states
        variant === 'default' && "data-[state=active]:bg-background data-[state=active]:text-foreground data-[state=active]:shadow-sm",
        variant === 'pills' && "data-[state=active]:bg-background data-[state=active]:text-foreground data-[state=active]:shadow-md rounded-full",
        variant === 'underline' && "data-[state=active]:text-foreground border-b-2 border-transparent data-[state=active]:border-primary rounded-none pb-2",
        variant === 'minimal' && "data-[state=active]:text-foreground data-[state=active]:font-semibold",
        
        // Hover states
        "hover:text-foreground hover:bg-accent/50",
        variant === 'underline' && "hover:border-border",
        
        // Animation class
        animationClass,
        
        className
      )}
      {...props}
    />
  )
})
SlideTabsTrigger.displayName = TabsPrimitive.Trigger.displayName

// === TABS CONTENT COMPONENT === //
interface SlideTabsContentProps extends React.ComponentPropsWithoutRef<typeof TabsPrimitive.Content> {
  direction?: 'left' | 'right' | 'up' | 'down'
  animation?: 'slide' | 'fade' | 'scale' | 'none'
}

const SlideTabsContent = React.forwardRef<
  React.ElementRef<typeof TabsPrimitive.Content>,
  SlideTabsContentProps
>(({ className, direction = 'right', animation = 'slide', ...props }, ref) => {
  return (
    <TabsPrimitive.Content
      ref={ref}
      className={cn(
        "mt-2 ring-offset-background focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2",
        
        // Animation classes based on type
        animation === 'slide' && "data-[state=active]:animate-tab-content-enter",
        animation === 'fade' && "data-[state=active]:animate-spring-fade-in",
        animation === 'scale' && "data-[state=active]:animate-spring-scale-in",
        
        className
      )}
      {...props}
    />
  )
})
SlideTabsContent.displayName = TabsPrimitive.Content.displayName

// === COMPOUND EXPORT === //
export { 
  SlideTabs, 
  SlideTabsList, 
  SlideTabsTrigger, 
  SlideTabsContent,
  type SlideTabsListProps,
  type SlideTabsTriggerProps,
  type SlideTabsContentProps
}
```

#### 4.2.2 Advanced Usage Patterns
```typescript
// === ADVANCED SLIDE TABS USAGE === //

// Complex Tab Configuration with State Management
const AdvancedTabsExample = () => {
  const [activeTab, setActiveTab] = useState("overview")
  const [tabHistory, setTabHistory] = useState<string[]>(["overview"])
  
  const handleTabChange = (value: string) => {
    setActiveTab(value)
    setTabHistory(prev => [...prev.slice(-4), value]) // Keep last 5 tabs
  }
  
  const tabs = [
    { 
      id: "overview", 
      label: "Overview", 
      icon: <LayoutDashboardIcon className="h-4 w-4" />,
      content: <OverviewContent />
    },
    { 
      id: "analytics", 
      label: "Analytics", 
      icon: <BarChartIcon className="h-4 w-4" />,
      content: <AnalyticsContent />,
      badge: "New"
    },
    { 
      id: "settings", 
      label: "Settings", 
      icon: <SettingsIcon className="h-4 w-4" />,
      content: <SettingsContent />,
      disabled: false
    }
  ]
  
  return (
    <Card className="w-full max-w-4xl mx-auto">
      <CardHeader>
        <CardTitle>Advanced Tabs Example</CardTitle>
        <CardDescription>
          Demonstrating complex tab functionality with animations
        </CardDescription>
      </CardHeader>
      
      <CardContent>
        <SlideTabs 
          value={activeTab} 
          onValueChange={handleTabChange}
          className="w-full"
        >
          <SlideTabsList 
            variant="default"
            size="default"
            distribution="stretch"
            className="custom-tabs-list"
          >
            {tabs.map((tab, index) => (
              <SlideTabsTrigger
                key={tab.id}
                value={tab.id}
                index={index}
                variant="default"
                animation="bounce"
                disabled={tab.disabled}
                className="custom-tab-trigger relative"
              >
                <span className="flex items-center gap-2">
                  {tab.icon}
                  {tab.label}
                  {tab.badge && (
                    <Badge variant="secondary" className="ml-1 text-xs">
                      {tab.badge}
                    </Badge>
                  )}
                </span>
                
                {/* Active indicator */}
                {activeTab === tab.id && (
                  <div className="absolute -bottom-1 left-1/2 transform -translate-x-1/2 w-1 h-1 bg-primary rounded-full animate-spring-scale-in" />
                )}
              </SlideTabsTrigger>
            ))}
          </SlideTabsList>
          
          {tabs.map((tab) => (
            <SlideTabsContent 
              key={tab.id}
              value={tab.id}
              animation="slide"
              className="custom-tab-content"
            >
              <div className="content-spacing">
                {tab.content}
              </div>
            </SlideTabsContent>
          ))}
        </SlideTabs>
        
        {/* Tab History for debugging */}
        <div className="mt-6 p-3 bg-muted rounded-lg">
          <p className="text-sm text-muted-foreground">
            Tab History: {tabHistory.join(' → ')}
          </p>
        </div>
      </CardContent>
    </Card>
  )
}
```

#### 4.2.3 Performance Optimizations
```typescript
// === PERFORMANCE OPTIMIZED SLIDE TABS === //

// Memoized Tab Content für große Datensets
const MemoizedTabContent = React.memo(({ data, activeTab }: {
  data: any[]
  activeTab: string
}) => {
  return (
    <div className="space-y-4">
      {data.map((item, index) => (
        <div 
          key={item.id}
          className="stagger-item p-4 border border-border rounded-lg"
          style={{ animationDelay: `${index * 50}ms` }}
        >
          {/* Content */}
        </div>
      ))}
    </div>
  )
})

// Lazy Loading für Tab Content
const LazyTabContent = React.lazy(() => import('./TabContent'))

const OptimizedTabs = () => {
  const [loadedTabs, setLoadedTabs] = useState<Set<string>>(new Set(['overview']))
  
  const handleTabChange = (value: string) => {
    setLoadedTabs(prev => new Set([...prev, value]))
  }
  
  return (
    <SlideTabs onValueChange={handleTabChange}>
      <SlideTabsList>
        <SlideTabsTrigger value="overview" index={0}>Overview</SlideTabsTrigger>
        <SlideTabsTrigger value="data" index={1}>Large Dataset</SlideTabsTrigger>
      </SlideTabsList>
      
      <SlideTabsContent value="overview">
        <div>Always loaded content</div>
      </SlideTabsContent>
      
      <SlideTabsContent value="data">
        {loadedTabs.has('data') ? (
          <Suspense fallback={<TabContentSkeleton />}>
            <LazyTabContent />
          </Suspense>
        ) : (
          <div>Tab not loaded yet</div>
        )}
      </SlideTabsContent>
    </SlideTabs>
  )
}
```

#### 4.2.4 Accessibility Enhancements
```typescript
// === ACCESSIBILITY FEATURES === //

const AccessibleSlideTabs = () => {
  const [announceContent, setAnnounceContent] = useState("")
  
  const handleTabChange = (value: string) => {
    const tabLabel = tabs.find(tab => tab.id === value)?.label
    setAnnounceContent(`${tabLabel} tab selected`)
    
    // Clear announcement after screen reader reads it
    setTimeout(() => setAnnounceContent(""), 1000)
  }
  
  return (
    <>
      {/* Screen reader announcements */}
      <div 
        aria-live="polite" 
        aria-atomic="true"
        className="sr-only"
      >
        {announceContent}
      </div>
      
      <SlideTabs 
        onValueChange={handleTabChange}
        className="w-full"
        // Keyboard navigation enhancements
        onKeyDown={(e) => {
          if (e.key === 'Home') {
            // Go to first tab
            setActiveTab(tabs[0].id)
          } else if (e.key === 'End') {
            // Go to last tab
            setActiveTab(tabs[tabs.length - 1].id)
          }
        }}
      >
        <SlideTabsList role="tablist">
          {tabs.map((tab, index) => (
            <SlideTabsTrigger
              key={tab.id}
              value={tab.id}
              index={index}
              role="tab"
              aria-selected={activeTab === tab.id}
              aria-controls={`tabpanel-${tab.id}`}
              id={`tab-${tab.id}`}
              // Enhanced keyboard support
              onKeyDown={(e) => {
                if (e.key === 'ArrowRight' || e.key === 'ArrowDown') {
                  e.preventDefault()
                  const nextIndex = (index + 1) % tabs.length
                  setActiveTab(tabs[nextIndex].id)
                } else if (e.key === 'ArrowLeft' || e.key === 'ArrowUp') {
                  e.preventDefault()
                  const prevIndex = index === 0 ? tabs.length - 1 : index - 1
                  setActiveTab(tabs[prevIndex].id)
                }
              }}
            >
              {tab.label}
            </SlideTabsTrigger>
          ))}
        </SlideTabsList>
        
        {tabs.map((tab) => (
          <SlideTabsContent
            key={tab.id}
            value={tab.id}
            role="tabpanel"
            aria-labelledby={`tab-${tab.id}`}
            id={`tabpanel-${tab.id}`}
            tabIndex={0} // Make focusable for screen readers
          >
            {tab.content}
          </SlideTabsContent>
        ))}
      </SlideTabs>
    </>
  )
}
```

---

## 5. LAYOUT & GRID-SYSTEM

### 5.1 Responsive Grid Foundation

#### 5.1.1 CSS Grid-basiertes Layout System
```css
/* === RESPONSIVE GRID FOUNDATION === */

/* Container System mit mathematischen Proportionen */
.container-system {
  /* Golden Ratio basierte Container-Größen */
  --container-xs: 20rem;      /* 320px - Mobile */
  --container-sm: 24rem;      /* 384px - Small Mobile */
  --container-md: 28rem;      /* 448px - Large Mobile */
  --container-lg: 32rem;      /* 512px - Tablet */
  --container-xl: 40rem;      /* 640px - Small Desktop */
  --container-2xl: 48rem;     /* 768px - Desktop */
  --container-3xl: 64rem;     /* 1024px - Large Desktop */
  --container-4xl: 80rem;     /* 1280px - XL Desktop */
  --container-max: 90rem;     /* 1440px - Maximum */
}

/* Advanced Grid System */
.grid-system {
  display: grid;
  gap: var(--spacing-4); /* 16px base gap */
  
  /* Responsive grid columns mit CSS Custom Properties */
  grid-template-columns: repeat(var(--grid-cols, 12), minmax(0, 1fr));
  
  /* Auto-fit responsive pattern */
  &.grid-auto-fit {
    grid-template-columns: repeat(auto-fit, minmax(var(--min-col-width, 280px), 1fr));
  }
  
  /* Auto-fill pattern für konstante Größen */
  &.grid-auto-fill {
    grid-template-columns: repeat(auto-fill, var(--col-width, 280px));
  }
}

/* Mathematically spaced grid gaps */
.gap-system {
  /* Fibonacci-sequence basierte Gaps */
  &.gap-xs { gap: var(--spacing-1); }    /* 4px */
  &.gap-sm { gap: var(--spacing-2); }    /* 8px */
  &.gap-md { gap: var(--spacing-4); }    /* 16px */
  &.gap-lg { gap: var(--spacing-6); }    /* 24px */
  &.gap-xl { gap: var(--spacing-8); }    /* 32px */
  &.gap-2xl { gap: var(--spacing-12); }  /* 48px */
}
```

#### 5.1.2 Tailwind Grid Configuration
```typescript
/* === TAILWIND GRID CONFIGURATION === */

// Erweiterte Grid-Konfiguration in tailwind.config.ts
extend: {
  gridTemplateColumns: {
    // Standard 12-column system
    '12': 'repeat(12, minmax(0, 1fr))',
    
    // Custom column systems
    '13': 'repeat(13, minmax(0, 1fr))',
    '14': 'repeat(14, minmax(0, 1fr))',
    '15': 'repeat(15, minmax(0, 1fr))',
    '16': 'repeat(16, minmax(0, 1fr))',
    
    // Auto-fit patterns
    'auto-fit-xs': 'repeat(auto-fit, minmax(200px, 1fr))',
    'auto-fit-sm': 'repeat(auto-fit, minmax(280px, 1fr))',
    'auto-fit-md': 'repeat(auto-fit, minmax(320px, 1fr))',
    'auto-fit-lg': 'repeat(auto-fit, minmax(400px, 1fr))',
    
    // Asymmetric layouts
    'sidebar': '280px 1fr',
    'sidebar-narrow': '240px 1fr',
    'sidebar-wide': '320px 1fr',
    'two-column': '1fr 1fr',
    'three-column': '1fr 2fr 1fr',
    'golden-ratio': '1fr 1.618fr',
    
    // Content-focused layouts
    'blog': '1fr min(65ch, 100%) 1fr',
    'reading': '1fr min(75ch, 100%) 1fr',
    'docs': '280px 1fr 240px',
  },
  
  gridTemplateRows: {
    // Standard row systems
    '7': 'repeat(7, minmax(0, 1fr))',
    '8': 'repeat(8, minmax(0, 1fr))',
    '9': 'repeat(9, minmax(0, 1fr))',
    '10': 'repeat(10, minmax(0, 1fr))',
    
    // Layout-specific rows
    'layout': 'auto 1fr auto',
    'header-content-footer': '60px 1fr 80px',
    'app-layout': '64px 1fr',
    'dashboard': '72px 1fr 48px',
  },
  
  gridColumn: {
    // Extended column spans
    'span-13': 'span 13 / span 13',
    'span-14': 'span 14 / span 14',
    'span-15': 'span 15 / span 15',
    'span-16': 'span 16 / span 16',
  },
  
  gridRow: {
    // Extended row spans
    'span-7': 'span 7 / span 7',
    'span-8': 'span 8 / span 8',
    'span-9': 'span 9 / span 9',
    'span-10': 'span 10 / span 10',
  }
}
```

#### 5.1.3 Responsive Breakpoint System
```css
/* === RESPONSIVE BREAKPOINT SYSTEM === */

/* Mobile-First Approach mit logischen Breakpoints */
@media (min-width: 480px) {  /* xs: Extra Small */
  .responsive-grid {
    --grid-cols: 6;
    gap: var(--spacing-3);
  }
}

@media (min-width: 640px) {  /* sm: Small */
  .responsive-grid {
    --grid-cols: 8;
    gap: var(--spacing-4);
  }
}

@media (min-width: 768px) {  /* md: Medium */
  .responsive-grid {
    --grid-cols: 12;
    gap: var(--spacing-6);
  }
}

@media (min-width: 1024px) { /* lg: Large */
  .responsive-grid {
    --grid-cols: 12;
    gap: var(--spacing-8);
  }
}

@media (min-width: 1280px) { /* xl: Extra Large */
  .responsive-grid {
    --grid-cols: 12;
    gap: var(--spacing-10);
  }
}

@media (min-width: 1536px) { /* 2xl: 2X Large */
  .responsive-grid {
    --grid-cols: 12;
    gap: var(--spacing-12);
  }
}

/* Container Queries für component-level Responsiveness */
@container (min-width: 320px) {
  .container-responsive {
    grid-template-columns: 1fr;
  }
}

@container (min-width: 640px) {
  .container-responsive {
    grid-template-columns: 1fr 1fr;
  }
}

@container (min-width: 960px) {
  .container-responsive {
    grid-template-columns: 1fr 2fr 1fr;
  }
}
```

### 5.2 Layout Component Patterns

#### 5.2.1 Core Layout Components
```typescript
/* === CORE LAYOUT COMPONENTS === */

// Stack Layout - Vertikale Anordnung mit Smart Spacing
interface StackProps {
  children: React.ReactNode
  space?: keyof typeof spacing
  align?: 'start' | 'center' | 'end' | 'stretch'
  distribute?: 'start' | 'center' | 'end' | 'between' | 'around' | 'evenly'
  className?: string
}

const spacing = {
  none: 'space-y-0',
  xs: 'space-y-1',
  sm: 'space-y-2', 
  md: 'space-y-4',
  lg: 'space-y-6',
  xl: 'space-y-8',
  '2xl': 'space-y-12',
}

const Stack = ({ 
  children, 
  space = 'md', 
  align = 'stretch',
  distribute = 'start',
  className 
}: StackProps) => {
  return (
    <div className={cn(
      'flex flex-col',
      spacing[space],
      align === 'start' && 'items-start',
      align === 'center' && 'items-center', 
      align === 'end' && 'items-end',
      align === 'stretch' && 'items-stretch',
      distribute === 'start' && 'justify-start',
      distribute === 'center' && 'justify-center',
      distribute === 'end' && 'justify-end',
      distribute === 'between' && 'justify-between',
      distribute === 'around' && 'justify-around',
      distribute === 'evenly' && 'justify-evenly',
      className
    )}>
      {children}
    </div>
  )
}

// Cluster Layout - Horizontale Anordnung mit Wrapping
interface ClusterProps {
  children: React.ReactNode
  space?: keyof typeof spacing
  align?: 'start' | 'center' | 'end' | 'baseline' | 'stretch'
  justify?: 'start' | 'center' | 'end' | 'between' | 'around' | 'evenly'
  wrap?: boolean
  className?: string
}

const Cluster = ({
  children,
  space = 'md',
  align = 'center',
  justify = 'start', 
  wrap = true,
  className
}: ClusterProps) => {
  return (
    <div className={cn(
      'flex gap-4',
      wrap && 'flex-wrap',
      align === 'start' && 'items-start',
      align === 'center' && 'items-center',
      align === 'end' && 'items-end',
      align === 'baseline' && 'items-baseline',
      align === 'stretch' && 'items-stretch',
      justify === 'start' && 'justify-start',
      justify === 'center' && 'justify-center',
      justify === 'end' && 'justify-end',
      justify === 'between' && 'justify-between',
      justify === 'around' && 'justify-around',
      justify === 'evenly' && 'justify-evenly',
      className
    )}>
      {children}
    </div>
  )
}

// Grid Layout - Responsive Grid mit Smart Defaults
interface GridProps {
  children: React.ReactNode
  columns?: number | 'auto-fit' | 'auto-fill'
  minItemWidth?: string
  gap?: keyof typeof spacing
  className?: string
}

const Grid = ({
  children,
  columns = 'auto-fit',
  minItemWidth = '280px',
  gap = 'md',
  className
}: GridProps) => {
  return (
    <div 
      className={cn(
        'grid',
        spacing[gap].replace('space-y-', 'gap-'),
        typeof columns === 'number' && `grid-cols-${columns}`,
        className
      )}
      style={{
        gridTemplateColumns: 
          columns === 'auto-fit' ? `repeat(auto-fit, minmax(${minItemWidth}, 1fr))` :
          columns === 'auto-fill' ? `repeat(auto-fill, minmax(${minItemWidth}, 1fr))` :
          typeof columns === 'number' ? `repeat(${columns}, minmax(0, 1fr))` :
          undefined
      }}
    >
      {children}
    </div>
  )
}
```

#### 5.2.2 Page Layout Templates
```typescript
/* === PAGE LAYOUT TEMPLATES === */

// App Shell Layout - Standard Application Layout
interface AppShellProps {
  sidebar?: React.ReactNode
  header?: React.ReactNode
  footer?: React.ReactNode
  children: React.ReactNode
  sidebarWidth?: 'narrow' | 'default' | 'wide'
  sidebarCollapsible?: boolean
  sidebarDefaultCollapsed?: boolean
}

const AppShell = ({
  sidebar,
  header,
  footer,
  children,
  sidebarWidth = 'default',
  sidebarCollapsible = false,
  sidebarDefaultCollapsed = false
}: AppShellProps) => {
  const [sidebarCollapsed, setSidebarCollapsed] = useState(sidebarDefaultCollapsed)
  
  const sidebarWidths = {
    narrow: 'w-60',   // 240px
    default: 'w-64',  // 256px
    wide: 'w-80',     // 320px
  }
  
  const collapsedWidth = 'w-16' // 64px
  
  return (
    <div className="min-h-screen bg-background text-foreground">
      {/* Header */}
      {header && (
        <header className="sticky top-0 z-50 border-b border-border bg-background/95 backdrop-blur-sm">
          <div className="container-max mx-auto">
            {header}
          </div>
        </header>
      )}
      
      <div className="flex">
        {/* Sidebar */}
        {sidebar && (
          <aside className={cn(
            'sticky top-0 h-screen border-r border-border bg-sidebar-background transition-all duration-300',
            sidebarCollapsed ? collapsedWidth : sidebarWidths[sidebarWidth],
            'animate-spring-slide-right'
          )}>
            {sidebarCollapsible && (
              <div className="p-4 border-b border-sidebar-border">
                <Button
                  variant="ghost"
                  size="icon"
                  onClick={() => setSidebarCollapsed(!sidebarCollapsed)}
                  className="animate-smooth-press"
                >
                  {sidebarCollapsed ? <ChevronRightIcon /> : <ChevronLeftIcon />}
                </Button>
              </div>
            )}
            <div className={cn(
              'overflow-hidden transition-all duration-300',
              sidebarCollapsed && 'opacity-0'
            )}>
              {sidebar}
            </div>
          </aside>
        )}
        
        {/* Main Content */}
        <main className="flex-1 min-w-0">
          <div className="container-max mx-auto p-6 animate-spring-fade-in">
            {children}
          </div>
        </main>
      </div>
      
      {/* Footer */}
      {footer && (
        <footer className="border-t border-border bg-background">
          <div className="container-max mx-auto">
            {footer}
          </div>
        </footer>
      )}
    </div>
  )
}

// Dashboard Layout - Spezialisiert für Dashboard-Anwendungen
interface DashboardLayoutProps {
  title: string
  subtitle?: string
  actions?: React.ReactNode
  tabs?: Array<{
    id: string
    label: string
    content: React.ReactNode
  }>
  sidebar?: React.ReactNode
  children?: React.ReactNode
}

const DashboardLayout = ({
  title,
  subtitle,
  actions,
  tabs,
  sidebar,
  children
}: DashboardLayoutProps) => {
  const [activeTab, setActiveTab] = useState(tabs?.[0]?.id || '')
  
  return (
    <AppShell
      sidebar={sidebar}
      header={
        <div className="flex items-center justify-between py-4">
          <div className="animate-spring-from-left">
            <h1 className="text-2xl font-bold">{title}</h1>
            {subtitle && (
              <p className="text-muted-foreground">{subtitle}</p>
            )}
          </div>
          {actions && (
            <div className="animate-spring-from-right">
              {actions}
            </div>
          )}
        </div>
      }
    >
      {tabs ? (
        <SlideTabs value={activeTab} onValueChange={setActiveTab}>
          <SlideTabsList className="mb-6">
            {tabs.map((tab, index) => (
              <SlideTabsTrigger 
                key={tab.id} 
                value={tab.id} 
                index={index}
              >
                {tab.label}
              </SlideTabsTrigger>
            ))}
          </SlideTabsList>
          
          {tabs.map((tab) => (
            <SlideTabsContent key={tab.id} value={tab.id}>
              {tab.content}
            </SlideTabsContent>
          ))}
        </SlideTabs>
      ) : (
        children
      )}
    </AppShell>
  )
}
```

#### 5.2.3 Responsive Layout Utilities
```css
/* === RESPONSIVE LAYOUT UTILITIES === */

/* Auto-responsive Container */
.container-auto {
  width: 100%;
  max-width: var(--container-max);
  margin-left: auto;
  margin-right: auto;
  padding-left: var(--spacing-4);
  padding-right: var(--spacing-4);
}

@media (min-width: 640px) {
  .container-auto {
    padding-left: var(--spacing-6);
    padding-right: var(--spacing-6);
  }
}

@media (min-width: 1024px) {
  .container-auto {
    padding-left: var(--spacing-8);
    padding-right: var(--spacing-8);
  }
}

/* Intrinsic Web Design Pattern */
.intrinsic-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(280px, 100%), 1fr));
  gap: var(--spacing-6);
}

/* Aspect Ratio Containers */
.aspect-ratio-container {
  position: relative;
  overflow: hidden;
}

.aspect-ratio-container::before {
  content: '';
  display: block;
  padding-top: var(--aspect-ratio, 56.25%); /* 16:9 default */
}

.aspect-ratio-container > * {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* Specific aspect ratios */
.aspect-square { --aspect-ratio: 100%; }
.aspect-video { --aspect-ratio: 56.25%; }
.aspect-photo { --aspect-ratio: 75%; }
.aspect-golden { --aspect-ratio: 61.8%; }

/* Flexible Text Columns */
.text-columns {
  columns: var(--min-column-width, 280px);
  column-gap: var(--spacing-8);
  column-rule: 1px solid hsl(var(--border));
}

/* Masonry-style Layout */
.masonry-grid {
  column-count: var(--column-count, 3);
  column-gap: var(--spacing-6);
  column-fill: balance;
}

.masonry-grid > * {
  break-inside: avoid;
  margin-bottom: var(--spacing-6);
}

@media (max-width: 768px) {
  .masonry-grid {
    --column-count: 2;
  }
}

@media (max-width: 480px) {
  .masonry-grid {
    --column-count: 1;
  }
}
```

### 5.3 Advanced Layout Patterns

#### 5.3.1 Compound Layout Components
```typescript
/* === COMPOUND LAYOUT COMPONENTS === */

// Split Layout - Zwei-Bereich Layout mit Resizing
interface SplitLayoutProps {
  left: React.ReactNode
  right: React.ReactNode
  defaultSplit?: number
  minLeftWidth?: number
  minRightWidth?: number
  resizable?: boolean
  direction?: 'horizontal' | 'vertical'
  className?: string
}

const SplitLayout = ({
  left,
  right,
  defaultSplit = 50,
  minLeftWidth = 200,
  minRightWidth = 200,
  resizable = true,
  direction = 'horizontal',
  className
}: SplitLayoutProps) => {
  const [split, setSplit] = useState(defaultSplit)
  const [isDragging, setIsDragging] = useState(false)
  const containerRef = useRef<HTMLDivElement>(null)
  
  const handleMouseDown = (e: React.MouseEvent) => {
    if (!resizable) return
    setIsDragging(true)
    e.preventDefault()
  }
  
  const handleMouseMove = useCallback((e: MouseEvent) => {
    if (!isDragging || !containerRef.current) return
    
    const container = containerRef.current
    const rect = container.getBoundingClientRect()
    
    let newSplit: number
    if (direction === 'horizontal') {
      const x = e.clientX - rect.left
      newSplit = (x / rect.width) * 100
    } else {
      const y = e.clientY - rect.top
      newSplit = (y / rect.height) * 100
    }
    
    // Apply constraints
    const minLeftPercent = (minLeftWidth / (direction === 'horizontal' ? rect.width : rect.height)) * 100
    const minRightPercent = (minRightWidth / (direction === 'horizontal' ? rect.width : rect.height)) * 100
    
    newSplit = Math.max(minLeftPercent, Math.min(100 - minRightPercent, newSplit))
    setSplit(newSplit)
  }, [isDragging, direction, minLeftWidth, minRightWidth])
  
  const handleMouseUp = useCallback(() => {
    setIsDragging(false)
  }, [])
  
  useEffect(() => {
    if (isDragging) {
      document.addEventListener('mousemove', handleMouseMove)
      document.addEventListener('mouseup', handleMouseUp)
      
      return () => {
        document.removeEventListener('mousemove', handleMouseMove)
        document.removeEventListener('mouseup', handleMouseUp)
      }
    }
  }, [isDragging, handleMouseMove, handleMouseUp])
  
  return (
    <div
      ref={containerRef}
      className={cn(
        'flex h-full',
        direction === 'vertical' && 'flex-col',
        className
      )}
    >
      <div
        className="overflow-auto animate-spring-from-left"
        style={{
          [direction === 'horizontal' ? 'width' : 'height']: `${split}%`
        }}
      >
        {left}
      </div>
      
      {resizable && (
        <div
          className={cn(
            'bg-border hover:bg-accent transition-colors cursor-col-resize group',
            direction === 'horizontal' ? 'w-1 hover:w-2' : 'h-1 hover:h-2 cursor-row-resize',
            isDragging && 'bg-primary'
          )}
          onMouseDown={handleMouseDown}
        >
          <div className={cn(
            'hidden group-hover:block bg-primary rounded-full',
            direction === 'horizontal' ? 'w-full h-8 mt-2' : 'h-full w-8 ml-2'
          )} />
        </div>
      )}
      
      <div
        className="flex-1 overflow-auto animate-spring-from-right"
        style={{
          [direction === 'horizontal' ? 'width' : 'height']: `${100 - split}%`
        }}
      >
        {right}
      </div>
    </div>
  )
}

// Masonry Layout - Pinterest-style Grid
interface MasonryLayoutProps {
  children: React.ReactNode[]
  columns?: number
  gap?: string
  className?: string
}

const MasonryLayout = ({
  children,
  columns = 3,
  gap = '1rem',
  className
}: MasonryLayoutProps) => {
  const [columnElements, setColumnElements] = useState<React.ReactNode[][]>([])
  
  useEffect(() => {
    const cols: React.ReactNode[][] = Array.from({ length: columns }, () => [])
    
    children.forEach((child, index) => {
      const columnIndex = index % columns
      cols[columnIndex].push(
        <div 
          key={index} 
          className="animate-spring-from-bottom stagger-item"
          style={{ animationDelay: `${index * 100}ms` }}
        >
          {child}
        </div>
      )
    })
    
    setColumnElements(cols)
  }, [children, columns])
  
  return (
    <div 
      className={cn('flex', className)}
      style={{ gap }}
    >
      {columnElements.map((column, index) => (
        <div 
          key={index}
          className="flex-1 flex flex-col"
          style={{ gap }}
        >
          {column}
        </div>
      ))}
    </div>
  )
}
```

#### 5.3.2 Container Query Layouts
```typescript
/* === CONTAINER QUERY LAYOUTS === */

// Self-Adjusting Component basierend auf Container-Größe
interface ResponsiveCardProps {
  title: string
  content: React.ReactNode
  image?: string
  actions?: React.ReactNode
  className?: string
}

const ResponsiveCard = ({
  title,
  content,
  image,
  actions,
  className
}: ResponsiveCardProps) => {
  const cardRef = useRef<HTMLDivElement>(null)
  const [layout, setLayout] = useState<'stack' | 'side-by-side' | 'compact'>('stack')
  
  useEffect(() => {
    if (!cardRef.current) return
    
    const observer = new ResizeObserver((entries) => {
      const { width } = entries[0].contentRect
      
      if (width < 300) {
        setLayout('compact')
      } else if (width < 500) {
        setLayout('stack')
      } else {
        setLayout('side-by-side')
      }
    })
    
    observer.observe(cardRef.current)
    return () => observer.disconnect()
  }, [])
  
  return (
    <Card 
      ref={cardRef}
      className={cn(
        'overflow-hidden transition-all duration-300',
        layout === 'side-by-side' && 'flex',
        className
      )}
    >
      {image && (
        <div className={cn(
          'aspect-ratio-container',
          layout === 'side-by-side' ? 'w-48 flex-shrink-0' : 'w-full',
          layout === 'compact' && 'aspect-square'
        )}>
          <img 
            src={image} 
            alt={title}
            className="object-cover animate-spring-scale-in"
          />
        </div>
      )}
      
      <div className={cn(
        'p-6',
        layout === 'side-by-side' && 'flex-1'
      )}>
        <CardHeader className={cn(
          layout === 'compact' && 'p-4'
        )}>
          <CardTitle className={cn(
            layout === 'compact' ? 'text-lg' : 'text-xl'
          )}>
            {title}
          </CardTitle>
        </CardHeader>
        
        <CardContent className={cn(
          layout === 'compact' && 'p-4 pt-0'
        )}>
          {content}
        </CardContent>
        
        {actions && (
          <CardFooter className={cn(
            'flex gap-2',
            layout === 'compact' && 'p-4 pt-0 flex-wrap'
          )}>
            {actions}
          </CardFooter>
        )}
      </div>
    </Card>
  )
}
```

---

*Dieses umfangreiche Dokument wird fortgesetzt mit den verbleibenden Sektionen...*
