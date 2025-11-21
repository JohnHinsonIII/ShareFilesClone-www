# SecureShare File Sharing Platform - Recreation Prompt

## Complete Prompt for Regenerating the Application

Use this prompt with Claude or another AI assistant to recreate the SecureShare file sharing and collaboration platform from scratch.

---

## Main Prompt

```
Create a comprehensive, enterprise-grade file sharing and collaboration web application similar to OpenText Core Share with the following specifications:

## CORE FEATURES TO IMPLEMENT

### 1. Dashboard & Navigation
- Create a professional header with logo, user profile dropdown, and notification bell
- Implement a sidebar with navigation items:
  * Dashboard (with stats cards and recent activity feed)
  * My Files (main file browser)
  * Shared with Me
  * Recent files
  * Storage usage indicator with progress bar
- Design should be clean, modern, and professional using a blue color scheme

### 2. File Management System
- File upload interface with:
  * Drag-and-drop upload area with visual feedback
  * Multi-file upload support
  * File type icons (PDF, Word, Excel, PowerPoint, images, text files)
  * Progress indicators for uploads
  * File size display in KB/MB/GB
- File organization features:
  * Grid view and list view toggle
  * Create new folders functionality
  * File/folder cards with hover effects
  * Action menu button (three dots) on each file card
  * File metadata display (size, date modified)

### 3. Search and Filter
- Search bar with icon
- Real-time search filtering across file names
- Search input should be responsive and intuitive

### 4. File Sharing Capabilities
- Share modal with:
  * Email input for sharing with specific users
  * Permission level selector (Can view, Can edit, Can comment)
  * Link generation with copy button
  * Security options:
    - Password protection toggle
    - Expiration date toggle
  * "Get Link" section with shareable URL
- Toast notifications for successful actions

### 5. Collaboration Features
- Comments and activity tracking (shown in activity feed)
- User avatars with initials
- Recent activity display with:
  * Activity icons
  * User names and actions
  * Timestamps (e.g., "2 hours ago", "yesterday")

### 6. Statistics Dashboard
- Stat cards showing:
  * Total Files count
  * Shared Files count
  * Collaborators count
- Each stat card with distinct color accent (blue, green, orange)

### 7. Modal System
- Reusable modal component structure
- Modals for:
  * File sharing
  * Create new folder
- Modal backdrop with click-outside-to-close
- Close button (X) in modal header

### 8. Responsive Design
- Mobile-first approach
- Breakpoints for tablet and desktop
- Collapsible sidebar on mobile
- Responsive grid layout for file cards

## TECHNICAL REQUIREMENTS

### HTML Structure
- Semantic HTML5 elements
- Accessibility attributes (ARIA labels)
- Proper heading hierarchy
- Form elements with labels

### CSS Styling
- CSS custom properties (CSS variables) for theming:
  * --primary-color: #0066cc
  * --secondary-color: #4a90e2
  * --success-color: #28a745
  * --danger-color: #dc3545
  * --warning-color: #ffc107
  * --light-bg: #f8f9fa
  * --dark-bg: #343a40
  * --border-color: #dee2e6
  * --text-primary: #212529
  * --text-secondary: #6c757d

- Modern CSS features:
  * CSS Grid for layouts
  * Flexbox for component alignment
  * Transitions and animations
  * Box shadows for depth
  * Border radius for rounded corners
  * Hover effects on interactive elements

### JavaScript Functionality
- Pure vanilla JavaScript (no frameworks required for POC)
- Event handlers for:
  * File upload (input change and drag-drop)
  * View toggle (grid/list)
  * Modal open/close
  * Search/filter
  * Navigation between sections
  * Notifications

- Functions to implement:
  * showSection(section) - Navigate between dashboard views
  * toggleView(view) - Switch between grid and list view
  * handleFileUpload(event) - Process file uploads
  * handleDrop(event) - Handle drag-and-drop
  * searchFiles() - Filter files based on search input
  * openModal(modalName) - Open specific modal
  * closeModal(modalName) - Close modal
  * showNotification(message, type) - Display toast notifications
  * shareFile() - Share file logic
  * createFolder() - Create new folder
  * copyLink() - Copy share link to clipboard

- LocalStorage for:
  * Saving uploaded files list
  * User preferences
  * Recent activity

### Icons
- Use inline SVG icons for:
  * File types (document, PDF, spreadsheet, presentation, image)
  * Navigation items (dashboard, files, shared, clock)
  * Actions (upload, download, share, delete, search)
  * User interface (close, menu, notifications)

## DESIGN SPECIFICATIONS

### Color Palette
- Primary: Blue (#0066cc)
- Secondary: Light Blue (#4a90e2)
- Success: Green (#28a745)
- Danger: Red (#dc3545)
- Warning: Orange (#ffc107)
- Background: Light gray (#f8f9fa)
- Text: Dark gray (#212529)
- Secondary Text: Medium gray (#6c757d)

### Typography
- Font family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif
- Heading sizes: 1.5rem - 2rem
- Body text: 1rem
- Small text: 0.875rem
- Line height: 1.6

### Spacing
- Section padding: 2rem
- Card padding: 1.5rem
- Button padding: 10px 20px
- Gap between elements: 1rem - 2rem

### Animations
- Transition duration: 0.3s
- Easing: ease-out
- Hover transform: translateY(-2px) for cards
- Slide-in animation for notifications

## SAMPLE DATA TO INCLUDE

### Sample Files (6 files)
1. Project Proposal.docx - 2.4 MB - 2 days ago
2. Q4 Report.pdf - 5.1 MB - 1 week ago
3. Budget 2024.xlsx - 856 KB - 3 days ago
4. Presentation.pptx - 12.3 MB - 5 days ago
5. Team Photo.jpg - 3.8 MB - 1 week ago
6. Meeting Notes.txt - 24 KB - 2 weeks ago

### Activity Feed (3 items)
1. Sarah Johnson uploaded "Q4 Report.pdf" - 2 hours ago
2. Mike Davis shared "Project Proposal.docx" with you - 5 hours ago
3. Emily Chen commented on "Design Mockups.fig" - Yesterday

### Statistics
- Total Files: 247
- Shared Files: 15
- Collaborators: 8

## OUTPUT REQUIREMENTS

Create a single, standalone HTML file that includes:
1. All HTML structure
2. Complete CSS in <style> tags
3. All JavaScript in <script> tags
4. Inline SVG icons
5. Fully functional interactive elements
6. Responsive design that works on all screen sizes
7. Professional, polished appearance
8. Smooth animations and transitions

The application should be production-ready in appearance while serving as a proof-of-concept for the core features of an enterprise file sharing platform.

Make it visually impressive, highly functional, and easy to extend with backend integration in the future.
```

---

## Additional Customization Prompts

### If you want to add specific features:

#### 1. Add Version Control
```
Add a version history feature to the file sharing application:
- Create a "Versions" tab in file details
- Display list of versions with timestamps and users
- Show version numbers (v1.0, v1.1, etc.)
- Add "Restore this version" button
- Show file size changes between versions
- Add compare versions functionality
```

#### 2. Add Advanced Search
```
Enhance the search functionality with:
- Advanced search modal with filters
- Filter by file type (document, image, spreadsheet, etc.)
- Filter by date range (today, this week, this month, custom)
- Filter by file size (< 1MB, 1-10MB, > 10MB)
- Filter by owner/shared by
- Save search queries
- Recent searches dropdown
```

#### 3. Add Collaboration Features
```
Add real-time collaboration indicators:
- Show who is currently viewing a file
- Display user avatars on files being edited
- Add presence indicators (online/offline)
- Create a collaboration panel showing active users
- Add @mention functionality in comments
- Show typing indicators
```

#### 4. Add Mobile Features
```
Optimize for mobile devices:
- Add bottom navigation bar for mobile
- Implement swipe gestures for file actions
- Add pull-to-refresh functionality
- Create mobile-optimized file upload from camera
- Add offline mode with sync when online
- Implement touch-friendly controls
```

#### 5. Add Admin Panel
```
Create an administration section with:
- User management table
- Storage usage charts
- Activity logs and audit trail
- Security settings panel
- Policy configuration interface
- Bulk operations for users
- Export reports functionality
```

---

## Styling Variations

### Option 1: Dark Mode
```
Add dark mode toggle with:
- Dark background colors (#1a1a1a, #2d2d2d)
- Light text on dark background
- Adjusted shadows and borders
- Toggle switch in user menu
- Persist preference in localStorage
- Smooth transition between modes
```

### Option 2: Material Design
```
Convert to Material Design style:
- Use Material Design elevation levels
- Implement Material Design color system
- Add ripple effects on buttons
- Use Material Design icons
- Floating action button for primary actions
- Material Design cards with raised appearance
```

### Option 3: Glassmorphism
```
Apply glassmorphism design trend:
- Frosted glass effect on cards
- Backdrop blur filters
- Semi-transparent backgrounds
- Light borders with subtle colors
- Depth through layering
- Vibrant gradient backgrounds
```

---

## Backend Integration Prompts

### For REST API Integration
```
Add backend API integration:
- Create fetch API calls for all operations
- Implement JWT authentication
- Add loading states during API calls
- Handle API errors gracefully
- Add retry logic for failed requests
- Implement pagination for file lists
- Add real-time updates via WebSocket
- Cache API responses in IndexedDB
```

### For Firebase Integration
```
Integrate with Firebase:
- Set up Firebase authentication
- Use Firestore for metadata storage
- Use Firebase Storage for file uploads
- Implement real-time listeners
- Add user presence detection
- Set up security rules
- Implement offline persistence
```

---

## Testing Scenarios

### Manual Testing Checklist
```
Test the following scenarios:
1. Upload single file via button click
2. Upload multiple files via drag-and-drop
3. Switch between grid and list views
4. Search for files by name
5. Open and close modals
6. Create a new folder
7. Share a file with permission settings
8. Copy share link to clipboard
9. Toggle password protection and expiration
10. View file details on click
11. Navigate between different sections
12. Verify responsive design on mobile sizes
13. Check all hover effects and animations
14. Test keyboard navigation
15. Verify notification system
```

---

## Performance Optimization Prompts

```
Optimize the application for performance:
- Implement virtual scrolling for large file lists
- Lazy load file thumbnails
- Debounce search input
- Use CSS containment for file cards
- Minimize DOM manipulations
- Add service worker for caching
- Compress and optimize SVG icons
- Use requestAnimationFrame for animations
- Implement infinite scroll instead of pagination
```

---

## Accessibility Enhancement Prompts

```
Improve accessibility:
- Add ARIA labels to all interactive elements
- Ensure keyboard navigation works everywhere
- Add focus visible styles
- Implement skip navigation links
- Ensure color contrast meets WCAG AA standards
- Add screen reader announcements for actions
- Make all modals trapFocus
- Add alt text to all images
- Ensure form inputs have associated labels
```

---

## Security Enhancement Prompts

```
Add security features:
- Implement Content Security Policy headers
- Add CSRF token validation
- Sanitize all user inputs
- Implement rate limiting on actions
- Add file type validation
- Check file size limits
- Implement virus scanning simulation
- Add watermarks to sensitive documents
- Log all security-relevant actions
```

---

## Browser Compatibility

The application is designed to work on:
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+
- Mobile browsers (iOS Safari 14+, Chrome Android 90+)

---

## File Structure for Multi-File Version

If you want to split into separate files instead of single HTML:

```
project/
├── index.html
├── css/
│   ├── styles.css
│   ├── components.css
│   └── responsive.css
├── js/
│   ├── app.js
│   ├── fileManager.js
│   ├── modal.js
│   └── utils.js
├── assets/
│   ├── icons/
│   └── images/
└── README.md
```

---

## Deployment Options

### GitHub Pages
```
1. Create GitHub repository
2. Push HTML file to main branch
3. Enable GitHub Pages in settings
4. Access at: https://username.github.io/repo-name
```

### Netlify
```
1. Drag and drop HTML file to Netlify
2. Get instant deployment URL
3. Configure custom domain (optional)
```

### Vercel
```
1. Import GitHub repository
2. Auto-deploy on push
3. Get production URL
```

---

## License

This is a proof-of-concept application inspired by OpenText Core Share. For production use, ensure compliance with all relevant licenses and regulations.

---

**Created:** November 17, 2025
**Version:** 1.0
**Author:** Claude AI Assistant
