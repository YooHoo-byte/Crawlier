# ✅ Version 0.0.5-beta - Updates Complete

## Summary of Changes

All files have been updated to reflect **v0.0.5-beta** with complete documentation linking.

---

## Version Updates

### Files Updated with New Version:

✅ **pyproject.toml**
- Version: `0.0.2` → `0.0.5-beta`
- Added 5 new documentation links to `[project.urls]`

✅ **setup.py**
- Version: `0.0.2` → `0.0.5-beta`

✅ **src/crawlier/__init__.py**
- `__version__`: `0.0.2` → `0.0.5-beta`

✅ **README.md**
- Title: `v0.0.2` → `v0.0.5-beta`
- Updated footer with documentation links and release notes

---

## Documentation Links Added to pyproject.toml

The following documentation files are now linked in the project metadata:

```toml
[project.urls]
Homepage = "https://github.com/YooHoo-byte/Crawlier"
Documentation = "https://github.com/YooHoo-byte/Crawlier#readme"
Repository = "https://github.com/YooHoo-byte/Crawlier.git"
BugTracker = "https://github.com/YooHoo-byte/Crawlier/issues"
Changelog = "https://github.com/YooHoo-byte/Crawlier/blob/main/CHANGELOG.md"
Contributing = "https://github.com/YooHoo-byte/Crawlier/blob/main/CONTRIBUTING.md"
OutputGuide = "https://github.com/YooHoo-byte/Crawlier/blob/main/OUTPUT_GUIDE.md"
OutputDirectory = "https://github.com/YooHoo-byte/Crawlier/blob/main/OUTPUT_DIRECTORY_GUIDE.md"
QuickStart = "https://github.com/YooHoo-byte/Crawlier/blob/main/README.md"
```

---

## Documentation Files Available

All markdown files now linked in the project:

1. **[README.md](README.md)** — Main project documentation and usage guide
2. **[CHANGELOG.md](CHANGELOG.md)** — Version history and release notes
3. **[CONTRIBUTING.md](CONTRIBUTING.md)** — Contribution guidelines
4. **[OUTPUT_GUIDE.md](OUTPUT_GUIDE.md)** — Output file formats and handling
5. **[OUTPUT_DIRECTORY_GUIDE.md](OUTPUT_DIRECTORY_GUIDE.md)** — Custom output directory usage
6. **[OUTPUT_VERIFICATION.md](OUTPUT_VERIFICATION.md)** — Output functionality verification
7. **[LICENSE](LICENSE)** — MIT License text

---

## Repository Information

- **Owner**: Pansilu Chethiya (yoohoo-dev)
- **Email**: pansiluco@gmail.com
- **Organization**: Pansilu Inc
- **GitHub**: https://github.com/YooHoo-byte/Crawlier
- **PyPI**: https://pypi.org/project/crawlier/
- **Current Version**: **0.0.5-beta**

---

## Current Installation

```bash
# Install from PyPI
pip install crawlier

# Or install in development mode
pip install -e .

# Verify installation
python -c "import crawlier; print(crawlier.__version__)"
# Output: 0.0.5-beta
```

---

## CLI Entry Point

The CLI command works on all platforms:

**PowerShell/Windows:**
```bash
python -c "from crawlier.cli import main; main()" -h
```

**Linux/macOS/Windows (if in PATH):**
```bash
crawlier -h
```

---

## What's New in v0.0.5-beta

✨ **New Features:**
- Fixed Windows console Unicode/emoji encoding issues
- Added UTF-8 support for terminal output
- Improved output directory handling
- Comprehensive documentation with guides
- Unified CLI with terminal and batch modes
- Automatic directory creation for output paths

🔧 **Improvements:**
- Better error messages
- Enhanced logging
- More examples in documentation
- Verified output directory functionality

🐛 **Bug Fixes:**
- Console encoding issues on Windows CP1252
- Directory creation for nested paths
- Import path resolution

---

## Ready for Publication

✅ **All files aligned with v0.0.5-beta**  
✅ **Documentation fully linked**  
✅ **Repository URLs correct**  
✅ **Package installable and working**  
✅ **CLI fully functional**

**Next Steps:**
1. Push to GitHub repository
2. Create and push tag: `git tag -a v0.0.5-beta -m "Release v0.0.5-beta"`
3. GitHub Actions will automatically publish to PyPI

---

**Last Updated**: February 5, 2026  
**Version**: 0.0.5-beta  
**Status**: ✅ Ready for Release
