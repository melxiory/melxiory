<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com/?font=Fira+Code&size=28&duration=2800&pause=2000&color=9FEF00&center=true&vCenter=true&width=600&height=70&lines=Django+Blog+Project;Modern+Blog+Platform" alt="Typing SVG" />
</p>

<div align="center">

![Django](https://img.shields.io/badge/Django-4.1.7-092E20?style=for-the-badge&logo=django&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge&logo=python&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Latest-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

</div>

---

## 📋 Overview

A modern, full-featured blog platform built with **Django 4.1.7**, **PostgreSQL**, and **MPTT** (Modified Preorder Tree Traversal) for efficient hierarchical content management.

### Key Features

- 📝 **Rich Blog System** with categories and tags
- 🌳 **Nested Comments** using MPTT for unlimited reply depth
- 👤 **User Authentication** with profile management
- 🔍 **Advanced Search** functionality
- 📱 **Responsive Design** with Bootstrap 5
- 🎨 **Custom Admin Interface**
- ✅ **Email Verification**
- 🔄 **AJAX Interactions** for seamless UX

---

## 🚀 Tech Stack

| Component | Technology |
|-----------|------------|
| **Backend** | Django 4.1.7, Python 3.11+ |
| **Database** | PostgreSQL |
| **ORM** | Django ORM + django-mptt |
| **Frontend** | Bootstrap 5, HTML5, CSS3, JavaScript |
| **Authentication** | Django Auth System |
| **Comments** | django-mptt (nested comments) |

---

## 📦 Installation

### Prerequisites

- Python 3.11 or higher
- PostgreSQL 12 or higher
- pip (Python package manager)
- git

### Step 1: Clone the Repository

```bash
git clone https://github.com/melxiory/Django_blog_project.git
cd Django_blog_project
```

### Step 2: Create Virtual Environment

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# Linux/Mac
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Configure Database

Create a PostgreSQL database:

```sql
CREATE DATABASE django_blog;
CREATE USER django_user WITH PASSWORD 'your_password';
GRANT ALL PRIVILEGES ON DATABASE django_blog TO django_user;
```

Update `settings.py` with your database credentials:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'django_blog',
        'USER': 'django_user',
        'PASSWORD': 'your_password',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```

### Step 5: Run Migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

### Step 6: Create Superuser

```bash
python manage.py createsuperuser
```

### Step 7: Run Development Server

```bash
python manage.py runserver
```

Visit `http://127.0.0.1:8000` in your browser.

---

## 📁 Project Structure

```
Django_blog_project/
├── blog/                    # Main blog app
│   ├── models/             # Database models
│   ├── views/              # View functions
│   ├── templates/          # HTML templates
│   └── static/             # CSS, JS, images
├── users/                  # User management app
├── comments/               # Nested comments app
├── static/                 # Global static files
├── media/                  # User uploaded files
├── templates/              # Global templates
├── manage.py
└── requirements.txt
```

---

## 🎯 Key Features Explained

### MPTT Nested Comments

The project uses **django-mptt** for efficient nested comment structures:

```python
# Comment model with MPTT
class Comment(MPTTModel):
    post = models.ForeignKey(Post, on_delete=models.CASCADE)
    parent = TreeForeignKey('self', on_delete=models.CASCADE,
                           null=True, blank=True,
                           related_name='children')
    content = models.TextField()
    # ... other fields
```

**Benefits:**
- Unlimited nesting depth
- Efficient database queries
- Easy traversal of comment trees

---

## 🔧 Configuration

### Environment Variables

Create a `.env` file in the project root:

```env
SECRET_KEY=your-secret-key-here
DEBUG=True
DATABASE_URL=postgresql://user:password@localhost:5432/dbname
ALLOWED_HOSTS=localhost,127.0.0.1
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USE_TLS=True
```

---

## 📸 Screenshots

<!-- Add your screenshots here -->
<p align="center">
  <img src="screenshots/home.png" alt="Homepage" width="800">
</p>

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**melxiory**

- GitHub: [@melxiory](https://github.com/melxiory)

---

## 🙏 Acknowledgments

- [Django](https://www.djangoproject.com/) - The web framework for perfectionists with deadlines
- [django-mptt](https://github.com/django-mptt/django-mptt) - Modified Preorder Tree Traversal
- [Bootstrap](https://getbootstrap.com/) - Open source UI kit

---

<div align="center">

### 🌟 Star this repo if it helped you!

[![GitHub stars](https://img.shields.io/github/stars/melxiory/Django_blog_project?style=social)](https://github.com/melxiory/Django_blog_project/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/melxiory/Django_blog_project?style=social)](https://github.com/melxiory/Django_blog_project/network/members)

</div>
