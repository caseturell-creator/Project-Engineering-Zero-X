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

---

---

# HTTP Status Codes Reference

| Status Code | Meaning | Should You Be Concerned? | Common Causes |
|--------------|---------|--------------------------|---------------|
| 100-199 | Informational | No | Request is still being processed. |
| 200 OK | Request completed successfully. | No | Normal operation. |
| 201 Created | A new resource was created. | No | Successful POST request. |
| 204 No Content | Request succeeded with nothing to return. | No | Normal for some APIs. |
| 301 Moved Permanently | Resource has a new permanent location. | Usually No | URL changed. |
| 302 Found | Temporary redirect. | Usually No | Login redirects, temporary routing. |
| 304 Not Modified | Browser uses cached version. | No | Cache optimization. |
| 400 Bad Request | Invalid request sent by client. | Yes | Malformed URL or request. |
| 401 Unauthorized | Authentication required. | Yes | Login required or missing credentials. |
| 403 Forbidden | Access denied. | Yes | Permission issue. |
| 404 Not Found | Requested resource does not exist. | Yes | Missing page, CSS, JavaScript, image, or API endpoint. |
| 405 Method Not Allowed | Incorrect HTTP method used. | Yes | Using POST instead of GET (or vice versa). |
| 408 Request Timeout | Server waited too long. | Sometimes | Slow connection or server delay. |
| 429 Too Many Requests | Rate limit exceeded. | Yes | Too many requests in a short period. |
| 500 Internal Server Error | Server encountered an unexpected error. | Yes | Server-side bug. |
| 502 Bad Gateway | Invalid response from another server. | Yes | Reverse proxy or upstream server failure. |
| 503 Service Unavailable | Service temporarily unavailable. | Yes | Maintenance or overloaded server. |
| 504 Gateway Timeout | Upstream server failed to respond. | Yes | Network or backend timeout. |

---

## Quick Rule

| If You See... | Think... |
|---------------|----------|
| 200 | Resource loaded successfully. |
| 304 | Browser is using a cached copy. |
| 404 | The browser cannot find the requested resource. |
| 403 | The server knows who you are but will not allow access. |
| 500 | The server itself has failed. |
| 503 | The service is temporarily unavailable. |

---

## Case Study

During the TryHackMe investigation, the browser returned:

- `index-D3Qnehzi.css` → **404 Not Found**
- `index-DReG5tR5.js` → **404 Not Found**

Because the required CSS and JavaScript files could not be retrieved, the application never rendered and the browser displayed a blank white page.

---
---

# 6. The Investigation Process

## Overview

Successful troubleshooting begins with observation, not assumptions.

When an application behaves unexpectedly, the objective is not to immediately find a solution. Instead, the objective is to understand **why** the problem is occurring.

Professional engineers follow a structured investigation process that reduces guesswork and leads to evidence-based conclusions.

This process can be applied to web applications, operating systems, networks, APIs, databases, and cybersecurity investigations.

---

## Investigation Workflow

1. Observe the problem.
2. Gather evidence.
3. Form a hypothesis.
4. Test the hypothesis.
5. Eliminate incorrect possibilities.
6. Identify the root cause.
7. Verify the solution.
8. Document the findings.

---

## Step 1 — Observe

Begin by describing exactly what is happening.

Examples:

- The webpage is completely blank.
- Images fail to load.
- A button does not respond.
- A login request fails.

Avoid making assumptions during this stage.

Record only what can be directly observed.

---

## Step 2 — Gather Evidence

Use available tools to collect information.

Examples include:

- Browser Developer Tools
- Console messages
- Network requests
- HTTP status codes
- Server responses
- Application logs

Evidence should always take priority over assumptions.

---

## Step 3 — Form a Hypothesis

Based on the available evidence, develop one or more possible explanations.

Example:

> "The application may not be loading because a required JavaScript file is missing."

A hypothesis is not a conclusion.

It is simply a possible explanation that must be tested.

---

## Step 4 — Test the Hypothesis

Perform actions that either support or reject the hypothesis.

Examples:

- Refresh the page.
- Inspect network requests.
- Check the Console.
- Verify resource loading.
- Compare expected and actual behavior.

Every test should provide additional evidence.

---

## Step 5 — Eliminate Possibilities

As evidence is collected, remove explanations that are no longer supported.

Example:

- Internet connection is working.
- Server responds with HTTP 200.
- HTML loads successfully.

These observations eliminate several possible causes.

---

## Step 6 — Identify the Root Cause

The root cause is the underlying issue responsible for the observed behavior.

In many cases, the visible symptom is only the final result of another failure occurring earlier in the process.

---

## Step 7 — Verify the Solution

After applying a fix, confirm that:

- The original problem is resolved.
- No additional issues have been introduced.
- The expected behavior has returned.

---

## Step 8 — Document the Findings

A complete investigation should always end with documentation.

Record:

- The problem.
- The investigation process.
- Evidence collected.
- Root cause.
- Resolution.
- Lessons learned.

Documentation allows future investigations to be completed more quickly and consistently.

---

## Engineering Principle

> Never troubleshoot by guessing.

> Observe.
>
> Gather evidence.
>
> Test.
>
> Conclude.

Following this process consistently produces more reliable results than relying on intuition alone.

---

---

# 7. Case Study - Debugging a Blank Web Application

## Objective

The purpose of this case study is to demonstrate how a structured investigation can identify the root cause of a web application failure.

Unlike theoretical examples, this investigation documents a real debugging session performed during a TryHackMe exercise.

---

## The Problem

After launching the provided Static Site, the browser displayed a completely blank white page.

There were:

- No visible error messages
- No loading indicator
- No application content

At first glance, it was impossible to determine whether the issue originated from:

- The browser
- The user's computer
- The web application
- The server
- The TryHackMe lab

---

## Initial Observation

The only confirmed symptom was:

> The webpage was completely blank.

At this stage, no assumptions were made regarding the cause.

---

## Investigation

### Step 1

Open Browser Developer Tools.

The Console was inspected first.

Result:

- No critical JavaScript exceptions were immediately visible.
- Several warnings appeared, but none explained the blank page.

Conclusion:

The Console alone did not identify the problem.

---

### Step 2

Inspect the Network tab.

The webpage was refreshed while monitoring all requests.

Initial observations:

- Multiple requests returned HTTP 200.
- The main document loaded successfully.

Conclusion:

The server was responding correctly.

---

### Step 3

Inspect the page source.

Viewing the HTML source revealed:

- A root application container.
- References to external CSS.
- References to external JavaScript.

This indicated that the webpage depended on JavaScript to render its content.

---

### Step 4

Continue investigating the Network tab.

Further inspection revealed two failed requests.

The browser attempted to download:

- CSS
- JavaScript

Both returned:

**404 Not Found**

---

## Root Cause

The browser successfully downloaded the HTML document.

However, the required CSS and JavaScript files were unavailable.

Without the JavaScript bundle, the application could not initialize.

As a result, nothing was rendered to the screen, producing a completely blank webpage.

---

## Resolution

The investigation determined that the issue was not caused by:

- Browser configuration
- Browser cache
- Internet connectivity
- User error

The evidence indicated that the required application assets were unavailable.

The issue was documented and prepared for reporting to the platform.

---

## Lessons Learned

This investigation demonstrated several important engineering principles.

- Symptoms are not root causes.
- Evidence is more reliable than assumptions.
- Browser Developer Tools provide critical diagnostic information.
- A blank webpage does not necessarily indicate a browser failure.
- Modern web applications depend on multiple interconnected resources.

Most importantly:

A structured investigation produces better results than guessing.

---

---

# 8. Module Summary

This module introduced the fundamentals of debugging modern web applications using browser developer tools.

Topics covered included:

- Browser Developer Tools
- Browser compatibility
- The investigation process
- HTTP status codes
- Structured troubleshooting
- Root cause analysis
- Real-world debugging techniques

Rather than memorizing solutions, the objective of this module was to develop a repeatable engineering methodology that can be applied across many technical disciplines.

---

# Key Takeaways

- Observe before acting.
- Gather evidence before forming conclusions.
- Use Developer Tools to investigate rather than guess.
- Understand what HTTP status codes communicate.
- Verify assumptions through testing.
- Document investigations for future reference.
- Focus on identifying the root cause rather than treating symptoms.

---

# End of Module

