# Chrome Extension Starter

Simple Chrome extension template.

## Stack

- **Language:** Vanilla JavaScript
- **APIs:** Chrome Extension APIs
- **Styling:** CSS

## Quick Start

```bash
# Create project directory
mkdir my-extension && cd my-extension

# Create the files (see below)
# Then load in Chrome:
# 1. Go to chrome://extensions
# 2. Enable "Developer mode"
# 3. Click "Load unpacked"
# 4. Select your extension folder
```

## Project Structure

```
my-extension/
├── manifest.json           # Extension config
├── popup.html              # Popup UI
├── popup.js                # Popup logic
├── popup.css               # Popup styles
├── content.js              # Content script (runs on pages)
├── background.js           # Background service worker
└── icons/
    ├── icon16.png
    ├── icon48.png
    └── icon128.png
```

## Key Files

### manifest.json

```json
{
  "manifest_version": 3,
  "name": "My Extension",
  "version": "1.0.0",
  "description": "A simple Chrome extension",
  
  "permissions": [
    "storage",
    "activeTab"
  ],
  
  "action": {
    "default_popup": "popup.html",
    "default_icon": {
      "16": "icons/icon16.png",
      "48": "icons/icon48.png",
      "128": "icons/icon128.png"
    }
  },
  
  "background": {
    "service_worker": "background.js"
  },
  
  "content_scripts": [
    {
      "matches": ["<all_urls>"],
      "js": ["content.js"],
      "css": []
    }
  ],
  
  "icons": {
    "16": "icons/icon16.png",
    "48": "icons/icon48.png",
    "128": "icons/icon128.png"
  }
}
```

### popup.html

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <link rel="stylesheet" href="popup.css">
</head>
<body>
  <div class="container">
    <h1>My Extension</h1>
    
    <div class="section">
      <label for="input">Enter something:</label>
      <input type="text" id="input" placeholder="Type here...">
    </div>
    
    <button id="saveBtn">Save</button>
    <button id="actionBtn">Do Something</button>
    
    <div id="status"></div>
  </div>
  
  <script src="popup.js"></script>
</body>
</html>
```

### popup.css

```css
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  width: 300px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  font-size: 14px;
}

.container {
  padding: 16px;
}

h1 {
  font-size: 18px;
  margin-bottom: 16px;
  color: #333;
}

.section {
  margin-bottom: 12px;
}

label {
  display: block;
  margin-bottom: 4px;
  color: #666;
  font-size: 12px;
}

input {
  width: 100%;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 14px;
}

input:focus {
  outline: none;
  border-color: #4285f4;
}

button {
  width: 100%;
  padding: 10px;
  margin-top: 8px;
  border: none;
  border-radius: 4px;
  font-size: 14px;
  cursor: pointer;
  transition: background 0.2s;
}

#saveBtn {
  background: #4285f4;
  color: white;
}

#saveBtn:hover {
  background: #3367d6;
}

#actionBtn {
  background: #34a853;
  color: white;
}

#actionBtn:hover {
  background: #2d8e47;
}

#status {
  margin-top: 12px;
  padding: 8px;
  border-radius: 4px;
  font-size: 12px;
  text-align: center;
}

#status.success {
  background: #e6f4ea;
  color: #137333;
}

#status.error {
  background: #fce8e6;
  color: #c5221f;
}
```

### popup.js

```javascript
document.addEventListener('DOMContentLoaded', () => {
  const input = document.getElementById('input');
  const saveBtn = document.getElementById('saveBtn');
  const actionBtn = document.getElementById('actionBtn');
  const status = document.getElementById('status');

  // Load saved value
  chrome.storage.sync.get(['savedValue'], (result) => {
    if (result.savedValue) {
      input.value = result.savedValue;
    }
  });

  // Save value
  saveBtn.addEventListener('click', () => {
    const value = input.value;
    chrome.storage.sync.set({ savedValue: value }, () => {
      showStatus('Saved!', 'success');
    });
  });

  // Do something on current page
  actionBtn.addEventListener('click', async () => {
    const [tab] = await chrome.tabs.query({ active: true, currentWindow: true });
    
    chrome.tabs.sendMessage(tab.id, { 
      action: 'doSomething',
      data: input.value 
    }, (response) => {
      if (response?.success) {
        showStatus('Done!', 'success');
      } else {
        showStatus('Failed', 'error');
      }
    });
  });

  function showStatus(message, type) {
    status.textContent = message;
    status.className = type;
    setTimeout(() => {
      status.textContent = '';
      status.className = '';
    }, 2000);
  }
});
```

### content.js

```javascript
// This runs on every page (based on manifest matches)

// Listen for messages from popup
chrome.runtime.onMessage.addListener((request, sender, sendResponse) => {
  if (request.action === 'doSomething') {
    try {
      // Do something on the page
      console.log('Extension received:', request.data);
      
      // Example: Highlight all links
      document.querySelectorAll('a').forEach(link => {
        link.style.backgroundColor = 'yellow';
      });
      
      sendResponse({ success: true });
    } catch (error) {
      sendResponse({ success: false, error: error.message });
    }
  }
  
  return true; // Keep message channel open for async response
});

// Run on page load
console.log('Extension content script loaded');
```

### background.js

```javascript
// Service worker - runs in background

// On install
chrome.runtime.onInstalled.addListener(() => {
  console.log('Extension installed');
  
  // Set default values
  chrome.storage.sync.set({ savedValue: '' });
});

// Listen for messages
chrome.runtime.onMessage.addListener((request, sender, sendResponse) => {
  if (request.action === 'backgroundTask') {
    // Handle background tasks
    console.log('Background task:', request);
    sendResponse({ success: true });
  }
  
  return true;
});
```

## Creating Icons

Use any image editor or online tool:
- [Favicon.io](https://favicon.io) - Generate from text/emoji
- [Icons8](https://icons8.com) - Free icons

Sizes needed:
- 16x16 (toolbar)
- 48x48 (extensions page)
- 128x128 (Chrome Web Store)

## Common Permissions

```json
{
  "permissions": [
    "storage",        // Save data
    "activeTab",      // Access current tab
    "tabs",           // Access all tabs
    "notifications",  // Show notifications
    "contextMenus",   // Right-click menu
    "alarms"          // Scheduled tasks
  ]
}
```

## Next Steps

1. Add more features to popup
2. Customize content script for specific sites
3. Add options page for settings
4. Publish to Chrome Web Store

## Debugging

1. Go to `chrome://extensions`
2. Click "Errors" on your extension
3. Click "Inspect views: popup" to debug popup
4. Use DevTools on any page to debug content script
