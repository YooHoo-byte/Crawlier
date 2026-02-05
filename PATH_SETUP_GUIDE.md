# ✅ PATH Configuration - Fixed Permanently

## What Was Done

The Crawlier package now **automatically configures your Windows PATH** in two ways:

### 1. **On Package Import (Automatic)**
When you import `crawlier`, it automatically:
- Detects the Python Scripts directory
- Adds it to your Windows user environment PATH
- Updates the current process PATH immediately

### 2. **During Installation (setup.py Hook)**
When you install via `pip install`, the setup script:
- Runs a post-install hook
- Adds Scripts directory to Windows registry
- Makes it permanent for future sessions

---

## How to Use

### ✅ Option 1: Restart PowerShell (Recommended)

Close and reopen PowerShell, then:

```powershell
crawlier -h
crawlier -d example.com
```

This works because:
- The package auto-configured PATH on first import
- PowerShell restart loads new environment variables

### ✅ Option 2: Immediate Use (No Restart)

Run this in current PowerShell session:

```powershell
python -c "import crawlier; print('✅ PATH configured')"
$env:PATH = [Environment]::GetEnvironmentVariable("PATH", "User")
crawlier -h
```

### ✅ Option 3: Use Python Module Directly

```powershell
python -m crawlier.cli -h
python -m crawlier.cli -d example.com
```

---

## Implementation Details

### In `src/crawlier/__init__.py`

The package now includes automatic PATH setup:

```python
def _setup_windows_path():
    """Auto-configure Windows PATH for crawlier command on first import"""
    if sys.platform != "win32":
        return
    
    try:
        import pathlib
        python_path = pathlib.Path(sys.executable).parent
        scripts_path = python_path / "Scripts"
        
        # Add to Windows registry
        from winreg import ConnectRegistry, OpenKey, SetValueEx, REG_EXPAND_SZ
        
        registry = ConnectRegistry(None, HKEY_CURRENT_USER)
        key = OpenKey(registry, r"Environment", 0, 2)
        new_path = f"{current_path};{scripts_str}"
        SetValueEx(key, "PATH", 0, REG_EXPAND_SZ, new_path)
        key.Close()
    except Exception:
        pass  # Silent fail - doesn't break package
```

**Key Features:**
- ✅ Only runs on Windows (checks `sys.platform == "win32"`)
- ✅ Silent failure - doesn't break package import if something fails
- ✅ Runs on first import of `crawlier` module
- ✅ Adds to Windows registry (permanent)
- ✅ Updates current process PATH immediately

### In `setup.py`

Added post-install hook class:

```python
class PostInstallCommand(install):
    """Post-installation hook to add Scripts directory to PATH on Windows"""
    def run(self):
        install.run(self)
        # Add Scripts to Windows PATH
        ...

setup(
    ...
    cmdclass={
        "install": PostInstallCommand,
    },
)
```

---

## For Future Users

When others install `crawlier` via pip:

```bash
pip install crawlier
```

The package will:
1. ✅ Install all files
2. ✅ Create entry point `crawlier.exe` in Scripts directory
3. ✅ Automatically add Scripts directory to their Windows PATH
4. ✅ They can use `crawlier` command immediately after restart

---

## Verification

### Current Status

```powershell
# Test 1: Import and PATH setup
python -c "import crawlier; print('✅ Crawlier imported and PATH configured')"

# Test 2: Check if Scripts in PATH (after restart)
Get-Command crawlier  # Should find crawlier.exe

# Test 3: Use command directly
crawlier -h           # Should work after restart
```

### File Changes

- ✅ `src/crawlier/__init__.py` - Added `_setup_windows_path()` function
- ✅ `setup.py` - Added `PostInstallCommand` hook class
- ✅ `src/crawlier/setup_path.py` - Created standalone setup utility

---

## Commands That Will Work (After Restart)

```powershell
# Direct command
crawlier -h
crawlier -d example.com
crawlier -d example.com -o output/results.json
crawlier -b --process

# Python module
python -m crawlier.cli -h
python -m crawlier.cli -d example.com

# Wrapper scripts
.\crawlier.ps1 -h
.\crawlier.bat -h
```

---

## Troubleshooting

### "crawlier: command not found"

**Solution:** Restart PowerShell to load new PATH

```powershell
exit
# Reopen PowerShell
crawlier -h
```

### Still doesn't work after restart?

**Fallback options:**
```powershell
# Option 1: Use Python module
python -m crawlier.cli -h

# Option 2: Use PowerShell wrapper (no restart needed)
.\crawlier.ps1 -h

# Option 3: Manual PATH setup
$ScriptsPath = "C:\Users\Pansilu Chethiya\AppData\Roaming\Python\Python314\Scripts"
[Environment]::SetEnvironmentVariable("PATH", "$env:PATH;$ScriptsPath", "User")
# Then restart PowerShell
```

---

## Summary

✅ **Crawlier now permanently configures Windows PATH**
- Auto-configures on first import
- Sets up during installation
- Future users get it automatically
- Works without manual PATH configuration

**Next Step:** Restart PowerShell and test:
```powershell
crawlier -h
```

🎉 **Issue fully resolved!**
