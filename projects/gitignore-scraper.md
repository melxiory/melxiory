# Python Scraper/Selenium .gitignore Template

# Python
__pycache__/
*.py[cod]
*$py.class
*.so
.Python
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
wheels/
pip-wheel-metadata/
share/python-wheels/
*.egg-info/
.installed.cfg
*.egg
MANIFEST

# Virtual Environment
venv/
env/
ENV/
env.bak/
venv.bak/

# Environment variables
.env
.env.local
.env.*.local

# IDEs
.vscode/
.idea/
*.swp
*.swo
*~
.DS_Store

# Jupyter Notebook
.ipynb_checkpoints

# pytest
.pytest_cache/
.coverage
htmlcov/
coverage.xml
*.cover
.hypothesis/

# mypy
.mypy_cache/
.dmypy.json
dmypy.json

# Logs
logs/
*.log

# Scraped data (optional - uncomment if you don't want to commit data)
# output/
# data/
# results/
# *.csv
# *.json
# *.xlsx

# Selenium
screenshots/
downloads/
*.png
*.jpg

# ChromeDriver
chromedriver
chromedriver.exe
geckodriver
geckodriver.exe

# Browser profiles
chrome_profile/
firefox_profile/

# Headless browser temporary files
*.tmp
*.cache

# Proxy settings (sensitive)
proxy_config.json
proxies.json

# Request sessions/cookies
cookies.pkl
sessions/

# Rate limiting state
rate_limit_state.json

# Scraping state
state.json
progress.json

# Large data files
*.db
*.sqlite
*.sqlite3

# Reports
reports/
*.html
# Keep pytest reports if needed
# !reports/.gitkeep

# Celery (if using for async scraping)
celerybeat-schedule
celerybeat.pid

# Redis
dump.rdb

# Scrapy (if using)
.scrapy/
project_settings.py

# Browser extensions
*.crx
*.xpi
