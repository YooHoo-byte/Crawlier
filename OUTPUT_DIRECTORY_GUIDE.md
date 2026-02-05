# Crawlier Output Directory Guide

## Quick Summary

✅ **Output directory functionality is working perfectly!**

By default, the crawler saves files to the **current working directory**. You can specify a custom output directory using the `-o` parameter, and the crawler will **automatically create the directory** if it doesn't exist.

## Examples

### Example 1: Default (Current Directory)

```bash
cd E:\Projects\MyCrawls
crawlier -d example.com
```

**Output:**
```
E:\Projects\MyCrawls\
├── crawl_results.json
├── crawl_results_report.txt
├── crawl_results_urls.csv
└── crawl_data.db
```

### Example 2: Custom Output Directory

```bash
crawlier -d example.com -o output/crawl_results.json
```

**Output:**
```
E:\Projects\MyCrawls\
└── output\
    ├── crawl_results.json
    ├── crawl_results_report.txt
    └── crawl_results_urls.csv
```

Plus database (default location):
```
E:\Projects\MyCrawls\
└── crawl_data.db
```

### Example 3: Custom Output Directory + Custom Database

```bash
crawlier -d example.com -o output/results/crawl_results.json --db output/results/crawl_data.db
```

**Output:**
```
E:\Projects\MyCrawls\
└── output\
    └── results\
        ├── crawl_results.json
        ├── crawl_results_report.txt
        ├── crawl_results_urls.csv
        └── crawl_data.db
```

## File Generation Details

### What Gets Created

When you run a crawl with `-o output/crawl_results.json`, the crawler automatically creates:

1. **`output/crawl_results.json`** — Complete crawl data (JSON format)
2. **`output/crawl_results_report.txt`** — Human-readable report
3. **`output/crawl_results_urls.csv`** — URL list in CSV format
4. **`--db` location** — SQLite database (default: root of current directory)

### Automatic Directory Creation

You don't need to create the output directory beforehand:

```bash
# This works even if 'data/2026' doesn't exist yet
crawlier -d example.com -o data/2026/crawl_results.json
# Automatically creates: data\ → 2026\ → crawl_results.json
```

### Nested Directory Support

You can use deeply nested paths:

```bash
crawlier -d example.com -o results/sites/example.com/2026-02/crawl_results.json
# Creates entire directory structure automatically
```

## Batch Mode Output

In batch mode, each domain gets its own output files:

```bash
crawlier -b --process
```

Creates per-domain output files in the **current directory**:

```
./
├── crawl_results_example_com.json
├── crawl_results_example_com_report.txt
├── crawl_results_example_com_urls.csv
├── crawl_results_example2_com.json
├── crawl_results_example2_com_report.txt
├── crawl_results_example2_com_urls.csv
└── crawl_data.db  (shared across all domains)
```

The batch mode is currently hardcoded to use `output/` for results (see `batch_crawler.py` line 61).

## Real-World Usage Patterns

### Pattern 1: Organize by Date

```bash
# Create dated directory
mkdir crawls\2026-02-05
cd crawls\2026-02-05

# Run crawls in that directory
crawlier -d example.com
crawlier -d example2.com

# Results go to: crawls\2026-02-05\
```

### Pattern 2: Organize by Domain

```bash
crawlier -d example.com -o example.com\crawl_results.json
crawlier -d example2.com -o example2.com\crawl_results.json

# Creates:
# example.com\crawl_results.json
# example.com\crawl_results_report.txt
# example.com\crawl_results_urls.csv
# example2.com\crawl_results.json
# etc...
```

### Pattern 3: Separate Databases

```bash
# Keep separate databases for different crawls
crawlier -d example.com -o results.json --db crawl_20260205.db
crawlier -d example.com -o results.json --db crawl_20260206.db

# Later, compare the two crawls
sqlite3 crawl_20260205.db "SELECT COUNT(*) FROM crawl_keywords;"
sqlite3 crawl_20260206.db "SELECT COUNT(*) FROM crawl_keywords;"
```

## Verifying Output

After running a crawl, verify files were created:

```bash
# List all output files
ls output\

# Check file size
(Get-ChildItem output\).Length

# View JSON structure
Get-Content output\crawl_results.json | ConvertFrom-Json | Format-List

# Read report
Get-Content output\crawl_results_report.txt
```

## Troubleshooting

### "Permission Denied" Error

If you get permission errors creating directories:
- Run PowerShell as Administrator
- Or use a different output directory (e.g., in Documents or Desktop)

### Files Not Created

If output files aren't appearing:
1. Check the crawl completed successfully (look for `[+] Results saved` message)
2. Verify the path doesn't have typos
3. Ensure you have write permissions to the parent directory

Example:
```bash
# Check if crawl succeeded
crawlier -d example.com -o test\output.json 2>&1 | tail -5
# Should show: "[+] Results saved to test\output.json"
```

### Mixed Locations

Output JSON/Report/CSV files respect the `-o` parameter directory.
The database file (specified with `--db`) goes to its own location:

```bash
# JSON/Report/CSV → output/
# DB → root/
crawlier -d example.com -o output/crawl_results.json

# JSON/Report/CSV → output/
# DB → output/ (same location)
crawlier -d example.com -o output/crawl_results.json --db output/crawl_data.db
```

## Summary

- ✅ Output directory is **automatically created**
- ✅ Works with **nested directory paths**
- ✅ `-o` parameter controls JSON/Report/CSV location
- ✅ `--db` parameter controls database location
- ✅ Both parameters support **relative and absolute paths**

The current implementation is fully functional and production-ready!
