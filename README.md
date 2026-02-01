# 📧 Scan to Email AI - PWA Documentation

A Progressive Web App that captures document images, extracts text using OCR, generates AI summaries with Claude, and creates Word documents that can be emailed via your device's default email app.

## 🌟 Features

### Core Functionality
- 📷 **Camera Integration** - Take photos with device camera or select from gallery
- 🔍 **Offline OCR** - Extract text from images using Tesseract.js (works offline)
- 🤖 **AI Summarization** - Generate detailed summaries using Claude API (requires internet)
- 📊 **Smart Grouping** - Automatically detects document headers (e.g., N109DR, N813DG)
- 📝 **Word Documents** - Creates professional .docx files with grouped summaries
- 📧 **Email Integration** - Opens default email app with pre-filled recipients and attachment
- 📱 **PWA Support** - Installable on Android & iOS as native-like app
- 🎨 **Custom Design** - Uses your uploaded icon throughout the app

### Advanced Features
- ✨ **Image Enhancement** - Auto-adjusts brightness/contrast for better OCR accuracy
- 💾 **Settings Storage** - Saves recipient emails and preferences locally
- 🔄 **Progress Tracking** - Visual progress bar with step-by-step status updates
- ⚠️ **Error Handling** - Clear error messages with retry options
- 🌐 **Offline Detection** - Warns when internet is needed for AI features
- 📋 **Multiple Recipients** - Send to multiple email addresses
- ⚙️ **Customizable Templates** - Edit email subject and body

---

## 🚀 Quick Start

### Prerequisites
- A modern web browser (Chrome, Safari, Edge, Firefox)
- Android or iOS device (for full PWA experience)
- Internet connection (for AI summarization)

### Installation Steps

#### 1. Setup Files
All files are ready in your project folder:
```
scan-to-email-ai/
├── index.html
├── manifest.json
├── service-worker.js
├── icon-192.png
├── icon-512.png
├── background.png
└── README.md
```

#### 2. Serve the App

**Option A: VS Code Live Server (Recommended)**
1. Open project folder in VS Code
2. Install "Live Server" extension
3. Right-click `index.html` → "Open with Live Server"
4. App will open at `http://localhost:5500` or similar

**Option B: Python Simple Server**
```bash
# Python 3
cd scan-to-email-ai
python -m http.server 8000

# Then open: http://localhost:8000
```

**Option C: Node.js http-server**
```bash
npm install -g http-server
cd scan-to-email-ai
http-server -p 8000

# Then open: http://localhost:8000
```

#### 3. Test in Browser
1. Open the app URL in your browser
2. You should see the splash screen with your icon
3. Navigate to Settings tab
4. Add recipient email addresses

---

## 📱 Installing as PWA

### On Android (Chrome/Edge)
1. Open the app in Chrome browser
2. Tap the menu (⋮) → "Add to Home Screen" or "Install App"
3. Confirm installation
4. App icon appears on home screen
5. Tap icon to launch as standalone app

### On iPhone (Safari)
1. Open the app in Safari browser
2. Tap the Share button (□↑)
3. Scroll down and tap "Add to Home Screen"
4. Edit name if desired → Tap "Add"
5. App icon appears on home screen
6. Tap icon to launch as standalone app

---

## 💡 How to Use

### First Time Setup

1. **Launch the App**
   - Splash screen displays with your icon
   - Main screen loads after 2 seconds

2. **Configure Settings**
   - Tap "⚙️ Settings" tab
   - Add recipient email addresses (one or more)
   - Optionally customize email subject/body
   - Settings save automatically

### Processing Documents

1. **Capture Images**
   - Tap "📷 Take or Select Photos"
   - Choose to take photos or select existing images
   - Add as many images as needed
   - Each image gets numbered

2. **Process Documents**
   - Tap "⚡ Process & Email" button
   - Watch progress bar:
     - Enhancing images (15%)
     - OCR text extraction (40%)
     - Detecting headers (45%)
     - AI summarization (80%)
     - Creating document (90%)
     - Opening email (100%)

3. **Review & Send Email**
   - Word document downloads automatically
   - Default email app opens with:
     - ✅ Recipients pre-filled
     - ✅ Subject pre-filled
     - ✅ Body pre-filled
   - **Manually attach the downloaded .docx file**
   - Review and tap "Send"

---

## 🎯 Understanding Header Detection

### How It Works
The app automatically detects document identifiers at the top of pages.

### Default Pattern
- Detects: `N` followed by digits and letters
- Examples: `N109DR`, `N 813DG`, `N12345AB`
- Case insensitive
- Spaces are normalized

### Grouping Logic
```
Image 1: "N109DR" → Group 1
Image 2: "N109DR" → Group 1 (same header)
Image 3: "N813DG" → Group 2 (new header)
```

### Word Document Output
```
Document Summaries
Generated: [Date/Time]

N109DR
[Detailed AI summary of all N109DR pages]

N813DG
[Detailed AI summary of all N813DG pages]
```

---

## ⚙️ Settings Configuration

### Recipient Emails
- **Multiple Recipients**: Add as many email addresses as needed
- **Validation**: Emails are validated before adding
- **Removal**: Tap × to remove an email
- **Storage**: Saved to browser's local storage

### Email Template

**Subject Line**
- Default: `Document Summaries - {date}`
- Use `{date}` placeholder for current date
- Example: "Monthly Reports - 1/31/2026"

**Email Body**
- Default: Pre-filled professional message
- Customize with your company info
- Supports multi-line text

---

## 🐛 Troubleshooting

### Images Not Processing
- Ensure images are well-lit
- Take photos straight-on (not at angle)
- Use high-resolution images
- OCR works best with printed text

### No Headers Detected
- Verify header format matches pattern (N109DR style)
- Ensure headers are at top of page
- Check that headers are clear and readable

### AI Summarization Failed
- Check internet connection
- Verify Claude API is accessible
- Try again (may be temporary API issue)

### Email Not Opening
- Ensure you have default email app configured
- Check device permissions for opening apps
- Download document and attach manually if needed

### App Won't Install
- Ensure using HTTPS (required for PWA)
- Check browser supports PWA (Chrome, Safari, Edge)
- Clear browser cache and try again

---

## 🔐 Privacy & Security

### Data Storage
- **Local Only**: All settings stored in browser
- **No Server**: No data sent to external servers (except Claude API)
- **No Tracking**: No analytics or tracking code
- **User Control**: Can clear all data via browser settings

### API Usage
- **Claude API**: Only used for summarization
- **Data Sent**: Only extracted text (not images)
- **Secure**: HTTPS encryption

---

## 🎨 Customization

### Changing Colors
Edit CSS variables in `index.html` (around line 20):

```css
:root {
  --primary-blue: #2d5f8d;
  --accent-cyan: #00d9ff;
  --dark-bg: #0a1929;
  /* ... etc */
}
```

### Changing Header Detection Pattern
Edit `index.html` around line 1010:

```javascript
// Current pattern
const headerPattern = /^N\s*\d{1,5}[A-Z]{1,3}/im;

// For "DOC-001" format
const headerPattern = /^DOC-\d{3}/i;
```

---

## 📊 Example Use Cases

- **Aviation**: Scan aircraft docs, group by tail number
- **Medical**: Scan patient charts, group by patient ID
- **Legal**: Scan case files, group by case number
- **Business**: Scan invoices, group by vendor

---

## 🆘 Common Questions

**Q: Can I use this without internet?**  
A: OCR works offline, but AI summarization requires internet.

**Q: How many images can I process?**  
A: 10-20 images recommended for best performance.

**Q: Does it support other languages?**  
A: Yes, change `'eng'` to other language codes in Tesseract.

**Q: Where are documents stored?**  
A: Only downloaded to your device, not stored by the app.

**Q: Can I use different email providers?**  
A: Yes! Works with any default email app (Gmail, Outlook, Apple Mail, etc.)

---

## 📝 Technical Stack

- **Frontend**: React 18
- **OCR**: Tesseract.js 5.0
- **AI**: Claude Sonnet 4 API
- **Documents**: docx.js 8.5
- **Files**: FileSaver.js 2.0
- **PWA**: Service Workers, Web App Manifest

---

## 🚀 Deployment Options

### For Production Use

**1. GitHub Pages**
- Free hosting
- HTTPS automatically provided
- Push code to GitHub repo
- Enable Pages in settings

**2. Netlify/Vercel**
- Free tier available
- Automatic HTTPS
- Drag-and-drop deployment
- Custom domain support

**3. Your Own Server**
- Requires HTTPS for PWA features
- Use Let's Encrypt for free SSL
- Configure proper MIME types

---

**Made with ❤️ using Claude AI**

🚀 **Ready to scan? Open the app and get started!**
