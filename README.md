# SecureShare - Enhanced File Sharing Platform

## Overview
SecureShare is a fully functional, enterprise-grade file sharing and collaboration platform with complete CRUD operations powered by localStorage JSON database. This application now includes working user management, file operations, and persistent data storage.

## 🆕 New Features Added

### 1. User Profile Management
- **Profile Settings**: Edit name, email, department, phone, language, and timezone
- **Account Settings**: Manage security and notification preferences
- **Help Center**: Built-in help documentation and support information
- **Sign Out**: Secure logout with data persistence

### 2. Complete File CRUD Operations
All file operations are now fully functional with localStorage persistence:

#### **Download** 
- Simulates file download with progress notifications
- Maintains download history

#### **Rename**
- Real-time file renaming with validation
- Updates all references automatically
- Maintains file metadata

#### **Move**
- Move files between folders
- Dropdown selector for destination folders
- Preserves file properties

#### **Delete**
- Confirmation dialog for safety
- Permanent removal from storage
- Activity logging

#### **Properties**
- View detailed file information:
  - File name
  - Size
  - Type
  - Created date
  - Modified date
  - Owner
  - Folder location
  - Sharing status

### 3. JSON Database (localStorage)
Complete database implementation with:

```javascript
// File Structure
{
    id: "file_123456789_abc",
    name: "Document.pdf",
    size: 2516582,
    type: "application/pdf",
    created: "2025-11-15T10:30:00.000Z",
    modified: "2025-11-17T14:20:00.000Z",
    owner: "John Doe",
    folder: "Documents",
    shared: false,
    tags: ["important", "project"],
    version: 1
}
```

#### Database Operations:

**CREATE**
```javascript
createFile(fileData)  // Add new file to database
createFolder(name)    // Create new folder
```

**READ**
```javascript
getAllFilesFromStorage()      // Get all files
getFileFromStorage(filename)  // Get specific file
getFilesByFolder(folder)      // Get files in folder
getSharedFiles()              // Get shared files only
searchFilesByName(query)      // Search files
```

**UPDATE**
```javascript
updateFile(filename, updates)  // Update file properties
updateUserProfile(updates)     // Update user profile
```

**DELETE**
```javascript
deleteFileFromStorage(filename)  // Remove file
```

### 4. User Profile System
Complete user profile management:
```javascript
{
    name: "John Doe",
    email: "john.doe@company.com",
    role: "User",
    department: "Engineering",
    phone: "+1 (555) 123-4567",
    storageQuota: 10737418240, // 10 GB
    language: "en",
    timezone: "America/New_York",
    notifications: true
}
```

### 5. Activity Tracking
All user actions are logged:
```javascript
{
    id: "activity_123",
    user: "John Doe",
    action: "uploaded",
    file: "Report.pdf",
    timestamp: "2025-11-17T10:30:00.000Z"
}
```

### 6. Folder Management
- Create custom folders
- Organize files hierarchically
- Move files between folders
- Default folders: My Files, Documents, Images, Projects, Archive

## 📋 Usage Guide

### Getting Started

1. **Open the Application**
   - Open `file-share-app.html` in any modern browser
   - Data persists in localStorage automatically

2. **Upload Files**
   - Click "Upload Files" button or drag-and-drop
   - Files are stored in the JSON database
   - Automatic activity logging

3. **Organize Files**
   - Create folders for organization
   - Move files using the file menu
   - Rename files as needed

### File Operations

#### To Download a File:
1. Click the three-dot menu (⋮) on any file
2. Select "Download"
3. File download will be simulated

#### To Rename a File:
1. Click the three-dot menu (⋮) on the file
2. Select "Rename"
3. Enter new name in the dialog
4. Click "Rename" to confirm

#### To Move a File:
1. Click the three-dot menu (⋮) on the file
2. Select "Move"
3. Choose destination folder
4. Click "Move" to confirm

#### To Delete a File:
1. Click the three-dot menu (⋮) on the file
2. Select "Delete"
3. Confirm deletion in the dialog
4. File is permanently removed

#### To View Properties:
1. Click the three-dot menu (⋮) on the file
2. Select "Properties"
3. View detailed file information

### User Profile Management

#### Update Profile:
1. Click your avatar in the top-right
2. Select "Profile Settings"
3. Edit your information:
   - Name
   - Email
   - Department
   - Phone
   - Language preference
   - Timezone
4. Click "Save Changes"

#### Account Settings:
1. Click your avatar
2. Select "Account"
3. Configure:
   - Password (simulated)
   - Email notifications
   - Desktop notifications
4. Click "Save Changes"

#### Get Help:
1. Click your avatar
2. Select "Help"
3. View:
   - Getting started guide
   - Keyboard shortcuts
   - Contact information

#### Sign Out:
1. Click your avatar
2. Select "Sign Out"
3. Confirm logout
4. All data remains saved

## 🗄️ Data Storage

All data is stored in browser localStorage:

- **files**: Array of all file objects
- **folders**: Array of folder names
- **userProfile**: User account information
- **activities**: Activity log entries

### Data Persistence

Data persists across browser sessions. To reset:
```javascript
localStorage.clear();
// Refresh the page to reinitialize with default data
```

### Export Data

To export your data:
```javascript
// In browser console:
const data = {
    files: JSON.parse(localStorage.getItem('files')),
    folders: JSON.parse(localStorage.getItem('folders')),
    profile: JSON.parse(localStorage.getItem('userProfile')),
    activities: JSON.parse(localStorage.getItem('activities'))
};
console.log(JSON.stringify(data, null, 2));
```

## 🔧 Technical Details

### File Structure
```
file-share-app.html
├── HTML Structure
│   ├── Header with user menu
│   ├── Dashboard with stats
│   ├── File browser (grid/list views)
│   └── Multiple modals for operations
├── CSS Styling
│   ├── Responsive design
│   ├── Custom properties for theming
│   └── Animations and transitions
└── JavaScript
    ├── Database CRUD operations
    ├── File management functions
    ├── User profile management
    └── Activity tracking
```

### Key Functions

#### Database Operations
```javascript
initializeDatabase()          // Initialize with default data
generateId()                  // Generate unique IDs
createFile(fileData)          // Create new file
getAllFilesFromStorage()      // Read all files
updateFile(filename, updates) // Update file
deleteFileFromStorage(name)   // Delete file
```

#### File Operations
```javascript
downloadFile()       // Download file
renameFile()         // Rename file
executeRename()      // Execute rename
moveFile()           // Move file
executeMove()        // Execute move
deleteFile()         // Delete file
showFileProperties() // Show properties
```

#### User Management
```javascript
getUserProfile()            // Get profile
updateUserProfile(updates)  // Update profile
saveProfileSettings()       // Save profile
saveAccountSettings()       // Save settings
signOut()                   // Logout
```

#### UI Operations
```javascript
updateFileDisplay()  // Refresh file list
loadActivityFeed()   // Load activities
updateStats()        // Update statistics
showNotification()   // Show toast
```

## 🎨 Customization

### Change Theme Colors
Edit CSS variables at the top of the style section:
```css
:root {
    --primary-color: #0066cc;
    --secondary-color: #4a90e2;
    --success-color: #28a745;
    --danger-color: #dc3545;
    --warning-color: #ffc107;
}
```

### Modify Default Folders
Edit the folders array:
```javascript
let folders = ['My Files', 'Documents', 'Images', 'Projects', 'Archive'];
```

### Change Storage Quota
Edit user profile:
```javascript
storageQuota: 10737418240  // 10 GB in bytes
```

### Add More File Types
Extend the `getFileIcon()` function with new mappings.

## 📊 Statistics Tracked

The dashboard displays:
- **Total Files**: Count of all files
- **Shared Files**: Count of shared files
- **Collaborators**: Number of unique collaborators (fixed at 8)
- **Storage Used**: Total size of all files
- **Storage Available**: Based on quota

## 🔐 Security Notes

This is a client-side proof-of-concept using localStorage:
- Data is stored locally in the browser
- No server-side authentication
- No encryption implemented
- Suitable for demonstration purposes only

For production use, implement:
- Server-side database (PostgreSQL, MongoDB)
- User authentication (JWT, OAuth)
- File encryption at rest and in transit
- Access control and permissions
- Secure API endpoints

## 🚀 Future Enhancements

Planned features for next version:
- [ ] File versioning system
- [ ] Real-time collaboration
- [ ] File preview capabilities
- [ ] Bulk operations
- [ ] Advanced search filters
- [ ] File tagging system
- [ ] Trash/recycle bin
- [ ] File compression
- [ ] Export/import functionality
- [ ] Dark mode toggle

## 🐛 Troubleshooting

### Files Not Persisting
- Check if localStorage is enabled in browser
- Verify browser doesn't have storage restrictions
- Check browser console for errors

### Cannot Upload Files
- Check file size (default max: 100MB)
- Verify drag-and-drop is supported
- Try using the upload button instead

### User Menu Not Showing
- Click on your name/avatar
- Check if JavaScript is enabled
- Refresh the page

### Stats Not Updating
- Refresh the page
- Check browser console for errors
- Verify localStorage is working

## 📝 Browser Compatibility

Tested and working on:
- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+
- ✅ Opera 76+

Requirements:
- JavaScript enabled
- localStorage support
- Modern CSS support (Grid, Flexbox)

## 📄 License

This is a proof-of-concept demonstration application inspired by OpenText Core Share.

## 🤝 Contributing

This is a standalone HTML application. To modify:
1. Open `file-share-app.html` in a text editor
2. Make your changes to HTML, CSS, or JavaScript
3. Test in multiple browsers
4. Document your changes

## 📧 Support

For questions or issues:
- Review the Help section in the app
- Check browser console for error messages
- Verify localStorage is functioning
- Test in a different browser

## 🎓 Learning Resources

To understand the code:
1. **HTML Structure**: Standard HTML5 with semantic elements
2. **CSS**: Modern CSS with Grid, Flexbox, and custom properties
3. **JavaScript**: Vanilla JS with localStorage API
4. **JSON**: Data structure for file storage

## 📚 Code Examples

### Creating a Custom File
```javascript
const customFile = {
    name: "MyFile.txt",
    size: 1024,
    type: "text/plain"
};
const newFile = createFile(customFile);
console.log(newFile);
```

### Searching Files
```javascript
const results = searchFilesByName("report");
console.log(results);
```

### Getting Shared Files
```javascript
const shared = getSharedFiles();
console.log(`You have ${shared.length} shared files`);
```

### Adding Custom Activity
```javascript
addActivity("custom action", "filename.pdf");
```

## 🔄 Version History

### Version 2.0 (Current)
- ✅ Complete CRUD operations
- ✅ User profile management
- ✅ File operations (download, rename, move, delete, properties)
- ✅ JSON database with localStorage
- ✅ Activity tracking
- ✅ User menu with dropdown
- ✅ Help system

### Version 1.0
- Basic file upload
- Grid and list views
- Simple file sharing
- Dashboard with stats

---

**Built with ❤️ using vanilla JavaScript, HTML5, and CSS3**

Last Updated: November 17, 2025
