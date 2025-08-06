# 🌟 Ecosystem Projects Repository

[![Auto-Update Projects](https://github.com/Uomi-network/uomi-website-ecosystem/actions/workflows/update-projects.yml/badge.svg)](https://github.com/Uomi-network/uomi-website-ecosystem/actions/workflows/update-projects.yml)

A GitHub-powered backend system for managing and showcasing ecosystem projects with automatic JSON generation and image hosting.

[![Auto-Update Projects](https://github.com/Uomi-network/uomi-website-ecosystem/actions/workflows/update-projects.yml/badge.svg)](https://github.com/Uomi-network/uomi-website-ecosystem/actions/workflows/update-projects.yml)
[![Projects Count](https://img.shields.io/badge/dynamic/json?color=brightgreen&label=projects&query=%24.count&url=https%3A%2F%2Fraw.githubusercontent.com%2FUomi-network%2Fuomi-website-ecosystem%2Fmain%2Fprojects.json)](https://raw.githubusercontent.com/Uomi-network/uomi-website-ecosystem/main/projects.json)

## 🚀 Quick Start

### For Project Owners

Want to add your project to the ecosystem? Follow these simple steps:

1. **Fork this repository**
2. **Create your project folder** in `/projects/`
3. **Add your files** (JSON + images)
4. **Submit a Pull Request**

That's it! Once merged, your project will automatically appear on the ecosystem website.

## 📁 Repository Structure

```
ecosystem-backend/
├── .github/workflows/
│   └── update-projects.yml     # Auto-generation workflow
├── projects/
│   ├── your-project/
│   │   ├── cover.webp         # Banner/background image
│   │   ├── primary.webp       # Logo/profile image
│   │   └── your-project.json  # Project metadata
│   └── another-project/
│       ├── cover.png          # Supports multiple formats
│       ├── primary.jpg        # PNG, JPG, JPEG, WEBP
│       └── project.json       # JSON with project details
├── projects.json              # 🤖 Auto-generated aggregated data
└── README.md
```

## 📋 Adding Your Project

### Step 1: Create Project Folder

Create a new folder in `/projects/` with your project name (use lowercase, hyphens for spaces):

```bash
projects/your-awesome-project/
```

### Step 2: Add Required Files

Your project folder **must** contain exactly these 3 files:

#### 🖼️ Images (Required)
- **`cover.*`** - Banner/background image (1200x400px recommended)
- **`primary.*`** - Logo/profile image (200x200px recommended, will be displayed as circle)

**Supported formats**: `.webp`, `.png`, `.jpg`, `.jpeg`

#### 📄 JSON Metadata (Required)
Create a JSON file named `{your-project-name}.json` with this structure:

```json
{
  "name": "Your Project Name",
  "description": "A compelling description of what your project does. Keep it concise but informative - this will be displayed on the project card.",
  "tags": ["DeFi", "NFT", "Gaming", "Infrastructure"],
  "primaryTag": "DeFi",
  "xLink": "https://twitter.com/yourproject",
  "websiteLink": "https://yourproject.com",
  "category": "App"
}
```

### Step 3: Field Specifications

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | ✅ | Your project's display name |
| `description` | string | ✅ | Brief project description (max 200 chars recommended) |
| `tags` | array | ✅ | Technology/category tags for filtering |
| `primaryTag` | string | ✅ | Main category tag (displayed prominently) |
| `xLink` | string | ❌ | Twitter/X profile URL |
| `websiteLink` | string | ❌ | Official website URL |
| `category` | string | ✅ | Either "App" or "Infra" |

### Step 4: Tag Guidelines

**Available Categories:**
- `App` - End-user applications, dApps, games
- `Infra` - Infrastructure, tools, protocols, SDKs

**Popular Tags:**
- **DeFi**: `DeFi`, `Trading`, `Lending`, `DEX`, `Yield`
- **Infrastructure**: `Dev Tooling`, `API`, `SDK`, `Analytics`, `Security`
- **Assets**: `NFT`, `RWA`, `Stablecoin`, `Payments`
- **Other**: `Gaming`, `Social`, `DAO`, `AI`, `Cross-chain`

## 🔄 Automatic Processing

### How It Works

1. **Push Detection**: GitHub Actions monitors the `/projects/` folder
2. **Validation**: Checks each project has required files (JSON + both images)
3. **Processing**: Generates public URLs for images and aggregates metadata
4. **Publication**: Creates/updates `projects.json` with all valid projects

### Generated Output

The system automatically creates `projects.json` accessible at:
```
https://raw.githubusercontent.com/Uomi-network/uomi-website-ecosystem/main/projects.json
```

**Example output:**
```json
{
  "projects": [
    {
      "id": "awesome-project",
      "name": "Awesome Project",
      "description": "Revolutionary DeFi protocol...",
      "tags": ["DeFi", "Yield"],
      "primaryTag": "DeFi",
      "category": "App",
      "xLink": "https://twitter.com/awesome",
      "websiteLink": "https://awesome.com",
      "coverImage": "https://raw.githubusercontent.com/.../cover.webp",
      "primaryImage": "https://raw.githubusercontent.com/.../primary.webp"
    }
  ],
  "lastUpdated": "2024-01-15T10:30:00.000Z",
  "count": 42,
  "generatedBy": "GitHub Actions"
}
```

## ✅ Quality Standards

### Image Requirements

- **Format**: WebP preferred (best compression), PNG/JPG acceptable
- **Cover Image**: 
  - Aspect ratio: ~3:1 (landscape)
  - Resolution: 1200x400px minimum
  - Max file size: 500KB
- **Primary Image**: 
  - Aspect ratio: 1:1 (square)
  - Resolution: 200x200px minimum
  - Max file size: 100KB

### Content Guidelines

- **Name**: Official project name, proper capitalization
- **Description**: 
  - Clear, professional language
  - Focus on core functionality
  - 50-150 words recommended
- **Links**: 
  - Must be active and official
  - Use HTTPS when available
- **Tags**: 
  - Use existing tags when possible
  - Maximum 5 tags per project
  - Relevant to actual functionality

## 🚫 Rejection Criteria

Projects will be excluded if they:

- ❌ Missing required files (JSON, cover image, or primary image)
- ❌ Invalid JSON format
- ❌ Broken or suspicious links
- ❌ Inappropriate content
- ❌ Copyright violations
- ❌ Images over size limits

## 🛠️ For Developers

### Frontend Integration

Use the generated JSON in your application:

```javascript
// Fetch projects data
const response = await fetch('https://raw.githubusercontent.com/Uomi-network/uomi-website-ecosystem/main/projects.json');
const data = await response.json();

// Access projects
const projects = data.projects;
const lastUpdate = data.lastUpdated;
const totalCount = data.count;
```

### API Endpoints

- **All Projects**: `https://raw.githubusercontent.com/Uomi-network/uomi-website-ecosystem/main/projects.json`
- **Individual Images**: `https://raw.githubusercontent.com/Uomi-network/uomi-website-ecosystem/main/projects/{project-id}/{image-file}`

### Local Development

```bash
# Clone repository
git clone https://github.com/Uomi-network/uomi-website-ecosystem.git
cd uomi-website-ecosystem

# Test workflow locally (requires Node.js)
node -e "
const fs = require('fs');
// ... (workflow script content)
"
```

## 📊 Statistics

- 🚀 **Auto-deployment**: Changes go live within 2-3 minutes
- 🖼️ **CDN-backed**: Images served via GitHub's global CDN
- 📱 **Mobile-optimized**: Responsive image serving
- 🔄 **Real-time**: JSON updates automatically on every push


## 📧 Support

### Adding Your Project
- **Issue**: Can't add your project? [Open an issue](../../issues/new)
- **Questions**: Review this README first, then ask in discussions

### Technical Issues
- **Workflow Failures**: Check [Actions tab](../../actions) for error details
- **Image Problems**: Verify file sizes and formats
- **JSON Errors**: Validate your JSON syntax


Individual project information and images remain property of their respective owners.

---

**🌟 Ready to showcase your project?** 

[**➡️ Add Your Project Now**](../../fork) | [**📋 View All Projects**](https://raw.githubusercontent.com/Uomi-network/uomi-website-ecosystem/main/projects.json) | [**🔧 Report Issues**](../../issues)
