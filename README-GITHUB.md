# SecureShare + GitHub Storage

A file sharing application with GitHub repository integration - upload files directly to your GitHub repository through a web interface.

## 🌟 Features

### File Management
- 📤 **Drag & Drop Upload**: Easy file upload interface
- 📁 **Local Storage**: Files stored locally before upload
- ☁️ **GitHub Integration**: Direct upload to GitHub repository
- 📊 **File Status Tracking**: See which files are local vs uploaded
- 🗑️ **File Management**: Delete files from local storage

### GitHub Integration
- ✅ **Personal Access Token**: Secure authentication
- 🔗 **Repository Connection**: Connect to any GitHub repository
- 📂 **Custom Paths**: Organize files in specific folders
- 🔍 **Connection Testing**: Verify GitHub setup before uploading
- 🔄 **Batch Upload**: Upload multiple files at once

## 🚀 Live Demo

**[Open Live Application](https://johnhinsoniii.github.io/ShareFilesClone-www/)**

## 📋 Setup Instructions

### Step 1: Create GitHub Personal Access Token

1. Go to GitHub → Settings → Developer settings
2. Click "Personal access tokens" → "Fine-grained tokens"
3. Click "Generate new token"
4. Configure token:
   - **Name**: SecureShare Token
   - **Expiration**: Choose duration
   - **Repository access**: Select repositories
   - **Permissions**: Enable "Contents" (Read and Write)
5. Click "Generate token"
6. **Copy the token** (starts with `ghp_`)

### Step 2: Create/Select GitHub Repository

1. Create a new repository or use existing one
2. Note your **username** and **repository name**
3. Ensure the repository is initialized with a README or has at least one commit

### Step 3: Configure Application

1. Open the SecureShare application
2. Fill in GitHub Configuration:
   - **Token**: Paste your personal access token
   - **Username**: Your GitHub username
   - **Repository**: Repository name (e.g., `my-documents`)
   - **Branch**: `main` (or your default branch)
   - **Path**: Optional folder path (e.g., `documents/`)
3. Click "💾 Save Configuration"
4. Click "🔍 Test Connection" to verify

### Step 4: Upload Files

1. Drag & drop files or click to browse
2. Files appear in the file list with "⏳ Local" status
3. Click "Upload" on individual files or "☁️ Upload All to GitHub"
4. Files will be uploaded to your repository
5. Status changes to "✓ On GitHub" when complete

## 🔐 Security

### Token Permissions

Your personal access token is stored locally in browser localStorage and is only used to authenticate with GitHub API. Recommended permissions:

- **Contents**: Read and Write (required)
- **Metadata**: Read-only (automatic)

### Best Practices

1. ✅ Use fine-grained tokens with minimal permissions
2. ✅ Set token expiration dates
3. ✅ Only grant access to specific repositories
4. ✅ Never share your token publicly
5. ✅ Revoke tokens if compromised

## 📁 File Organization

### Default Structure

```
your-repository/
└── documents/           # (or your custom path)
    ├── file1.pdf
    ├── file2.jpg
    └── file3.docx
```

### Custom Paths

You can organize files using custom paths:
- `documents/` - For general documents
- `images/` - For images
- `projects/2024/` - For project files
- Leave empty for root directory

## 🎯 Use Cases

### Personal Document Backup
- Upload important documents to GitHub
- Version control for your files
- Access from anywhere

### Team File Sharing
- Share files through GitHub repository
- Collaborate with team members
- Track file changes with Git history

### Project Documentation
- Upload project files and documentation
- Maintain organized file structure
- Easy access through GitHub interface

## 🛠️ Technical Details

### GitHub API Usage

The application uses GitHub's REST API v3:

```javascript
PUT /repos/{owner}/{repo}/contents/{path}
```

### File Upload Process

1. File selected via drag-drop or browse
2. File converted to Base64 encoding
3. API request sent to GitHub with:
   - Base64 content
   - Commit message
   - Branch name
   - File path
4. GitHub stores file and returns URL
5. Status updated in application

### Rate Limiting

- GitHub API: 5,000 requests/hour (authenticated)
- Application implements 1-second delay between uploads
- Monitor usage in GitHub Settings → Developer settings

## 📱 Browser Compatibility

- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+

Requirements:
- JavaScript enabled
- localStorage support
- FileReader API support

## 🐛 Troubleshooting

### "Connection failed" Error
- ✅ Check token is valid and not expired
- ✅ Verify repository exists and you have access
- ✅ Ensure token has Contents (Write) permission

### "Upload failed" Error
- ✅ Check file size (GitHub limit: 100MB)
- ✅ Verify branch name is correct
- ✅ Ensure path doesn't contain invalid characters
- ✅ Check rate limits haven't been exceeded

### "File already exists" Error
- Files with same name will overwrite
- Use different filenames or paths
- Or update the existing file intentionally

### Files Not Uploading
- ✅ Save GitHub configuration first
- ✅ Test connection before uploading
- ✅ Check browser console for errors
- ✅ Verify internet connection

## 📖 FAQs

**Q: Is my token secure?**
A: Tokens are stored in browser localStorage. Never share them publicly.

**Q: Can I upload large files?**
A: GitHub has a 100MB file size limit per file.

**Q: What happens to files after upload?**
A: They remain in GitHub repository and can be managed through GitHub interface.

**Q: Can I delete files from GitHub through the app?**
A: Currently only local deletion is supported. Delete from GitHub repository directly.

**Q: How do I revoke access?**
A: Go to GitHub → Settings → Developer settings → Tokens → Delete token

## 🔄 Updates & Roadmap

### Current Version
- ✅ GitHub file upload
- ✅ Local file management
- ✅ Connection testing
- ✅ Batch uploads
- ✅ Upload progress tracking

### Planned Features
- 📋 File listing from GitHub
- 🗑️ Delete files from GitHub
- 📝 File editing
- 📂 Folder creation
- 🔍 Search functionality

## 🤝 Contributing

To contribute or suggest features:
1. Fork the repository
2. Create a feature branch
3. Submit a pull request

## 📄 License

MIT License - Free to use for personal and commercial projects.

## 🙏 Credits

Built using:
- GitHub REST API v3
- Vanilla JavaScript
- HTML5 & CSS3
- FileReader API

---

**Built with ❤️ for seamless GitHub file management**

*Last Updated: November 21, 2025*
