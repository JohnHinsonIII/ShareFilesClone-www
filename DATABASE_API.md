# SecureShare - JSON Database API Documentation

## Overview
Complete reference for all CRUD operations in the SecureShare localStorage JSON database system.

---

## Database Structure

### Files Collection
```json
{
  "id": "file_1700000000000_abc123def",
  "name": "Document.pdf",
  "size": 2516582,
  "type": "application/pdf",
  "created": "2025-11-15T10:30:00.000Z",
  "modified": "2025-11-17T14:20:00.000Z",
  "owner": "John Doe",
  "folder": "Documents",
  "shared": false,
  "tags": ["important", "project"],
  "version": 1
}
```

### User Profile
```json
{
  "name": "John Doe",
  "email": "john.doe@company.com",
  "role": "User",
  "department": "Engineering",
  "phone": "+1 (555) 123-4567",
  "storageQuota": 10737418240,
  "language": "en",
  "timezone": "America/New_York",
  "notifications": true,
  "emailNotifications": true,
  "desktopNotifications": true
}
```

### Folders Collection
```json
[
  "My Files",
  "Documents",
  "Images",
  "Projects",
  "Archive"
]
```

### Activities Collection
```json
{
  "id": "activity_1700000000000_xyz789",
  "user": "John Doe",
  "action": "uploaded",
  "file": "Report.pdf",
  "timestamp": "2025-11-17T10:30:00.000Z"
}
```

---

## CRUD Operations

## CREATE Operations

### createFile(fileData)
Creates a new file entry in the database.

**Parameters:**
```javascript
fileData = {
  name: String,    // Required - File name
  size: Number,    // Required - File size in bytes
  type: String     // Required - MIME type
}
```

**Returns:** File object with generated ID and metadata

**Example:**
```javascript
const newFile = createFile({
  name: "Report.pdf",
  size: 2516582,
  type: "application/pdf"
});

// Returns:
{
  id: "file_1700000000000_abc123",
  name: "Report.pdf",
  size: 2516582,
  type: "application/pdf",
  created: "2025-11-17T10:30:00.000Z",
  modified: "2025-11-17T10:30:00.000Z",
  owner: "John Doe",
  folder: "My Files",
  shared: false,
  tags: [],
  version: 1
}
```

**Side Effects:**
- Saves to localStorage
- Adds activity log entry
- Updates statistics

---

### createFolder(folderName)
Creates a new folder if it doesn't exist.

**Parameters:**
```javascript
folderName: String  // Required - Folder name
```

**Returns:** Boolean (true if created, false if already exists)

**Example:**
```javascript
const success = createFolder("New Project");
// Returns: true (if folder didn't exist)

const duplicate = createFolder("Documents");
// Returns: false (folder already exists)
```

**Side Effects:**
- Saves to localStorage
- Adds activity log entry

---

## READ Operations

### getAllFilesFromStorage()
Retrieves all files from the database.

**Parameters:** None

**Returns:** Array of file objects

**Example:**
```javascript
const allFiles = getAllFilesFromStorage();
console.log(allFiles.length);  // e.g., 6
console.log(allFiles[0].name); // e.g., "Report.pdf"
```

---

### getFileFromStorage(filename)
Retrieves a specific file by name.

**Parameters:**
```javascript
filename: String  // Required - Exact file name
```

**Returns:** File object or undefined

**Example:**
```javascript
const file = getFileFromStorage("Report.pdf");
if (file) {
  console.log(file.size);  // 2516582
  console.log(file.owner); // "John Doe"
}
```

---

### getFilesByFolder(folderName)
Retrieves all files in a specific folder.

**Parameters:**
```javascript
folderName: String  // Required - Folder name
```

**Returns:** Array of file objects

**Example:**
```javascript
const docs = getFilesByFolder("Documents");
console.log(`${docs.length} files in Documents`);

docs.forEach(file => {
  console.log(file.name);
});
```

---

### getSharedFiles()
Retrieves all files that have been shared.

**Parameters:** None

**Returns:** Array of shared file objects

**Example:**
```javascript
const shared = getSharedFiles();
console.log(`You have ${shared.length} shared files`);

shared.forEach(file => {
  console.log(`${file.name} - shared with others`);
});
```

---

### searchFilesByName(query)
Searches for files by name (case-insensitive).

**Parameters:**
```javascript
query: String  // Required - Search term
```

**Returns:** Array of matching file objects

**Example:**
```javascript
const results = searchFilesByName("report");
// Returns all files with "report" in the name

results.forEach(file => {
  console.log(file.name);
});
```

---

### getUserProfile()
Retrieves the current user profile.

**Parameters:** None

**Returns:** User profile object

**Example:**
```javascript
const profile = getUserProfile();
console.log(profile.name);       // "John Doe"
console.log(profile.email);      // "john.doe@company.com"
console.log(profile.department); // "Engineering"
```

---

### getAllFolders()
Retrieves all folder names.

**Parameters:** None

**Returns:** Array of folder name strings

**Example:**
```javascript
const folders = getAllFolders();
console.log(folders);
// ["My Files", "Documents", "Images", "Projects", "Archive"]
```

---

### getAllActivities()
Retrieves all activity log entries.

**Parameters:** None

**Returns:** Array of activity objects (newest first)

**Example:**
```javascript
const activities = getAllActivities();
console.log(`${activities.length} activities logged`);

activities.forEach(activity => {
  console.log(`${activity.user} ${activity.action} ${activity.file}`);
});
```

---

## UPDATE Operations

### updateFile(filename, updates)
Updates properties of an existing file.

**Parameters:**
```javascript
filename: String,  // Required - Current file name
updates: Object    // Required - Properties to update
```

**Returns:** Updated file object or null if not found

**Example:**
```javascript
// Rename a file
const updated = updateFile("Report.pdf", {
  name: "Q4 Report.pdf"
});

// Move to different folder
const moved = updateFile("Budget.xlsx", {
  folder: "Archive"
});

// Mark as shared
const shared = updateFile("Presentation.pptx", {
  shared: true
});

// Multiple updates
const modified = updateFile("Document.docx", {
  name: "Updated Document.docx",
  folder: "Projects",
  shared: true,
  tags: ["important", "urgent"]
});
```

**Side Effects:**
- Updates modified timestamp
- Saves to localStorage

---

### updateUserProfile(updates)
Updates the user profile.

**Parameters:**
```javascript
updates: Object  // Required - Profile properties to update
```

**Returns:** Updated profile object

**Example:**
```javascript
// Update basic info
updateUserProfile({
  name: "Jane Smith",
  email: "jane.smith@company.com"
});

// Update preferences
updateUserProfile({
  language: "es",
  timezone: "America/Los_Angeles"
});

// Update settings
updateUserProfile({
  emailNotifications: false,
  desktopNotifications: true
});
```

**Side Effects:**
- Saves to localStorage
- Updates global userProfile variable

---

## DELETE Operations

### deleteFileFromStorage(filename)
Permanently deletes a file from the database.

**Parameters:**
```javascript
filename: String  // Required - File name to delete
```

**Returns:** None

**Example:**
```javascript
deleteFileFromStorage("Old Report.pdf");
```

**Side Effects:**
- Removes from localStorage
- Adds activity log entry
- Updates statistics

**⚠️ Warning:** This operation is permanent and cannot be undone!

---

## Utility Functions

### generateId()
Generates a unique ID for files and activities.

**Parameters:** None

**Returns:** String in format "file_timestamp_randomstring"

**Example:**
```javascript
const id = generateId();
console.log(id);  // "file_1700000000000_abc123def"
```

---

### saveFilesToStorage(files)
Saves the files array to localStorage.

**Parameters:**
```javascript
files: Array  // Required - Array of file objects
```

**Returns:** None

**Example:**
```javascript
const files = getAllFilesFromStorage();
// Modify files array
files.push(newFile);
saveFilesToStorage(files);
```

**Side Effects:**
- Updates localStorage
- Triggers stats update

---

### addActivity(action, file)
Logs a user activity.

**Parameters:**
```javascript
action: String,  // Required - Action description
file: String     // Required - File name
```

**Returns:** None

**Example:**
```javascript
addActivity("uploaded", "Report.pdf");
addActivity("shared", "Budget.xlsx");
addActivity("deleted", "Old File.txt");
addActivity("created folder", "New Project");
```

**Side Effects:**
- Adds to activities array
- Keeps only 50 most recent activities
- Saves to localStorage

---

## Advanced Queries

### Get Files by Type
```javascript
function getFilesByType(type) {
  const files = getAllFilesFromStorage();
  return files.filter(f => f.type.includes(type));
}

const pdfs = getFilesByType("pdf");
const images = getFilesByType("image");
const documents = getFilesByType("document");
```

---

### Get Files by Tag
```javascript
function getFilesByTag(tag) {
  const files = getAllFilesFromStorage();
  return files.filter(f => f.tags.includes(tag));
}

const important = getFilesByTag("important");
const projects = getFilesByTag("project");
```

---

### Get Files Modified Today
```javascript
function getFilesModifiedToday() {
  const files = getAllFilesFromStorage();
  const today = new Date().toDateString();
  return files.filter(f => {
    const modDate = new Date(f.modified).toDateString();
    return modDate === today;
  });
}

const todaysFiles = getFilesModifiedToday();
```

---

### Get Total Storage Used
```javascript
function getTotalStorageUsed() {
  const files = getAllFilesFromStorage();
  return files.reduce((total, file) => total + file.size, 0);
}

const totalBytes = getTotalStorageUsed();
console.log(`Total storage: ${formatFileSize(totalBytes)}`);
```

---

### Get Files by Owner
```javascript
function getFilesByOwner(owner) {
  const files = getAllFilesFromStorage();
  return files.filter(f => f.owner === owner);
}

const myFiles = getFilesByOwner("John Doe");
```

---

### Get Recently Modified Files
```javascript
function getRecentFiles(days = 7) {
  const files = getAllFilesFromStorage();
  const cutoff = Date.now() - (days * 24 * 60 * 60 * 1000);
  return files.filter(f => {
    return new Date(f.modified).getTime() > cutoff;
  }).sort((a, b) => {
    return new Date(b.modified) - new Date(a.modified);
  });
}

const lastWeek = getRecentFiles(7);
const lastMonth = getRecentFiles(30);
```

---

## Batch Operations

### Bulk Delete
```javascript
function bulkDelete(filenames) {
  filenames.forEach(name => {
    deleteFileFromStorage(name);
  });
  updateFileDisplay();
}

bulkDelete(["file1.txt", "file2.pdf", "file3.docx"]);
```

---

### Bulk Move
```javascript
function bulkMove(filenames, targetFolder) {
  filenames.forEach(name => {
    updateFile(name, { folder: targetFolder });
  });
  updateFileDisplay();
}

bulkMove(["doc1.pdf", "doc2.pdf"], "Archive");
```

---

### Bulk Share
```javascript
function bulkShare(filenames) {
  filenames.forEach(name => {
    updateFile(name, { shared: true });
  });
  updateFileDisplay();
}

bulkShare(["report1.pdf", "report2.pdf"]);
```

---

## Data Export/Import

### Export All Data
```javascript
function exportAllData() {
  const data = {
    files: JSON.parse(localStorage.getItem('files')),
    folders: JSON.parse(localStorage.getItem('folders')),
    profile: JSON.parse(localStorage.getItem('userProfile')),
    activities: JSON.parse(localStorage.getItem('activities'))
  };
  
  const json = JSON.stringify(data, null, 2);
  const blob = new Blob([json], { type: 'application/json' });
  const url = URL.createObjectURL(blob);
  
  const a = document.createElement('a');
  a.href = url;
  a.download = 'secureshare-backup.json';
  a.click();
}
```

---

### Import Data
```javascript
function importData(jsonString) {
  try {
    const data = JSON.parse(jsonString);
    
    if (data.files) localStorage.setItem('files', JSON.stringify(data.files));
    if (data.folders) localStorage.setItem('folders', JSON.stringify(data.folders));
    if (data.profile) localStorage.setItem('userProfile', JSON.stringify(data.profile));
    if (data.activities) localStorage.setItem('activities', JSON.stringify(data.activities));
    
    location.reload();
  } catch (error) {
    console.error('Import failed:', error);
  }
}
```

---

## Error Handling

### Safe File Operations
```javascript
function safeUpdateFile(filename, updates) {
  try {
    const result = updateFile(filename, updates);
    if (result) {
      return { success: true, data: result };
    } else {
      return { success: false, error: 'File not found' };
    }
  } catch (error) {
    return { success: false, error: error.message };
  }
}

const result = safeUpdateFile("Document.pdf", { name: "New Name.pdf" });
if (result.success) {
  console.log('Update successful');
} else {
  console.error('Update failed:', result.error);
}
```

---

## Performance Tips

1. **Batch Reads**: Get all files once and filter in memory
```javascript
const files = getAllFilesFromStorage();
const pdfs = files.filter(f => f.type.includes('pdf'));
const docs = files.filter(f => f.folder === 'Documents');
```

2. **Avoid Frequent Updates**: Collect changes and save once
```javascript
const files = getAllFilesFromStorage();
files.forEach(file => {
  if (file.folder === 'Old Folder') {
    file.folder = 'New Folder';
  }
});
saveFilesToStorage(files);
```

3. **Use Indexes**: Create lookup objects for frequent searches
```javascript
const filesByName = {};
getAllFilesFromStorage().forEach(file => {
  filesByName[file.name] = file;
});
// Fast lookup: filesByName['Report.pdf']
```

---

## Testing Examples

### Unit Test Example
```javascript
// Test file creation
console.log('Testing createFile...');
const testFile = createFile({
  name: 'Test.txt',
  size: 1024,
  type: 'text/plain'
});
console.assert(testFile.id, 'File should have an ID');
console.assert(testFile.owner === 'John Doe', 'Owner should be set');
console.log('✓ createFile test passed');

// Test file retrieval
console.log('Testing getFileFromStorage...');
const retrieved = getFileFromStorage('Test.txt');
console.assert(retrieved !== undefined, 'File should be retrievable');
console.assert(retrieved.size === 1024, 'Size should match');
console.log('✓ getFileFromStorage test passed');

// Test file update
console.log('Testing updateFile...');
const updated = updateFile('Test.txt', { size: 2048 });
console.assert(updated.size === 2048, 'Size should be updated');
console.log('✓ updateFile test passed');

// Test file deletion
console.log('Testing deleteFileFromStorage...');
deleteFileFromStorage('Test.txt');
const deleted = getFileFromStorage('Test.txt');
console.assert(deleted === undefined, 'File should be deleted');
console.log('✓ deleteFileFromStorage test passed');
```

---

## Best Practices

1. **Always validate input before creating/updating**
2. **Use meaningful file names**
3. **Add tags for better organization**
4. **Regularly check storage usage**
5. **Export data periodically for backup**
6. **Use folder structure effectively**
7. **Log important activities**
8. **Handle errors gracefully**

---

## Storage Limits

- **localStorage limit**: ~5-10 MB per domain (browser dependent)
- **Recommended max files**: 1000 files
- **Max file size** (simulated): 100 MB per file
- **Activity log**: Auto-limited to 50 entries

---

## Troubleshooting

### Clear All Data
```javascript
function resetDatabase() {
  if (confirm('This will delete ALL data. Continue?')) {
    localStorage.clear();
    location.reload();
  }
}
```

### Check Database Size
```javascript
function checkDatabaseSize() {
  let total = 0;
  for (let key in localStorage) {
    if (localStorage.hasOwnProperty(key)) {
      total += localStorage[key].length + key.length;
    }
  }
  console.log(`Database size: ${(total / 1024).toFixed(2)} KB`);
}
```

### Verify Data Integrity
```javascript
function verifyData() {
  const files = getAllFilesFromStorage();
  const folders = getAllFolders();
  
  files.forEach(file => {
    if (!file.id) console.error('File missing ID:', file.name);
    if (!file.name) console.error('File missing name:', file.id);
    if (!folders.includes(file.folder)) {
      console.warn('File in unknown folder:', file.name, file.folder);
    }
  });
  
  console.log('Data verification complete');
}
```

---

**Last Updated:** November 17, 2025
**Version:** 2.0
