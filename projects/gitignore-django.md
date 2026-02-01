# Django .gitignore Template

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

# Django
*.log
local_settings.py
db.sqlite3
db.sqlite3-journal
/static/
/media/

# If using PostgreSQL
*.psql

# If using MySQL
*.sql

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

# PyCharm
.idea/

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

# Selenium
screenshots/
downloads/

# Celery
celerybeat-schedule
celerybeat.pid

# Redis
dump.rdb
