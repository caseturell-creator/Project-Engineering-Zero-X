# Module 04 - Web Debugging

## 1. Introduction

Modern web applications are complex systems made up of many interconnected components. When a webpage fails to load correctly, the visible problem is often only a symptom of a deeper issue.

Effective engineers do not begin by guessing what is wrong. Instead, they collect evidence, eliminate possibilities, and identify the root cause through systematic investigation.

Modern browsers provide powerful developer tools that allow us to inspect how a webpage is built, how resources are loaded, how applications communicate with servers, and where failures occur.

The skills learned in this module apply to far more than web development. They are fundamental to cybersecurity, penetration testing, systems administration, quality assurance, and technical support.

This module introduces a structured methodology for debugging web applications using browser developer tools. Rather than focusing on memorizing fixes, the objective is to develop a repeatable investigation process that can be applied to any web application.

---

## 2. Learning Goals

After completing this module, you should be able to:

- Explain the purpose of browser developer tools.
- Navigate Chrome DevTools efficiently.
- Differentiate browser warnings from application errors.
- Inspect network requests.
- Interpret common HTTP status codes.
- Understand how modern JavaScript applications render webpages.
- Perform structured troubleshooting using evidence.
- Identify the root cause of common web application failures.
- Document technical findings clearly and professionally.

---

## 3. Why Web Debugging Matters

Every website depends on many different resources working together.

A single webpage may require:

- HTML
- CSS
- JavaScript
- Images
- Fonts
- APIs
- Databases
- External services

If even one critical resource fails to load, the entire application may stop functioning.

For this reason, engineers investigate systems as a collection of connected components rather than assuming a single point of failure.

Understanding how these components interact is the foundation of effective troubleshooting.
---

---

# 4. Browser Developer Tools

## Overview

Browser Developer Tools (DevTools) are built-in utilities that allow engineers to inspect, analyze, and debug web applications directly within the browser.

Rather than guessing why a webpage behaves a certain way, DevTools provides direct access to the information needed to investigate problems.

Whether you are a web developer, cybersecurity analyst, penetration tester, or IT technician, DevTools is one of the most valuable diagnostic tools available.

---

## Opening DevTools

Google Chrome provides several methods for opening Developer Tools.

### Keyboard Shortcuts

| Operating System | Shortcut |
|------------------|-----------|
| Windows / Linux | `F12` |
| Windows / Linux | `Ctrl + Shift + I` |
| macOS | `⌥ Option + ⌘ Command + I` |

### Menu Navigation

1. Open Chrome.
2. Click the three-dot menu.
3. Select **More Tools**.
4. Select **Developer Tools**.

---

## Primary DevTools Tabs

Although DevTools contains many panels, this module focuses on the tools most commonly used during web debugging.

| Tab | Purpose |
|------|----------|
| Elements | Inspect and modify the HTML and CSS of a webpage. |
| Console | View JavaScript output, warnings, and errors. |
| Network | Monitor every request made by the browser. |
| Sources | View the application's source files and scripts. |

---

## Choosing the Right Tool

Each DevTools tab answers a different type of question.

| Question | DevTools Tab |
|-----------|--------------|
| What does the webpage look like internally? | Elements |
| Are there JavaScript errors? | Console |
| Which files are loading? | Network |
| What source code is running? | Sources |

Understanding which tool answers which question is an important part of efficient troubleshooting.

Rather than clicking randomly through DevTools, experienced engineers select the tool that provides the information needed for the current investigation.

---

---

# 5. Browser Compatibility

## Overview

Although this module uses **Google Chrome** for demonstrations, the concepts presented apply to all modern web browsers.

Every major browser includes built-in developer tools that allow engineers to inspect webpages, monitor network activity, analyze application behavior, and diagnose problems.

While the layout and terminology may vary slightly between browsers, the investigative process remains the same.

---

## Common Browsers

| Browser | Developer Tools |
|----------|-----------------|
| Google Chrome | Chrome DevTools |
| Microsoft Edge | Edge DevTools |
| Mozilla Firefox | Firefox Developer Tools |
| Brave | Brave DevTools |
| Opera | Opera DevTools |
| Safari | Safari Web Inspector |

---

## Core Functionality

Regardless of the browser being used, developer tools generally provide access to:

- HTML inspection
- CSS inspection
- JavaScript debugging
- Network monitoring
- Performance analysis
- Storage and cookies
- Application resources

The names and appearance of these tools may differ, but their purpose remains consistent.

---

## Why Chrome?

Google Chrome is used throughout this module because it is one of the most widely adopted browsers in web development, cybersecurity, and penetration testing.

Many educational platforms, documentation, and security tools assume the use of Chrome or another Chromium-based browser.

Learning Chrome DevTools provides a strong foundation that can easily be transferred to other browsers.

---

## Key Takeaway

The goal is not to learn one browser.

The goal is to develop a repeatable debugging process that can be applied regardless of which browser is available.
