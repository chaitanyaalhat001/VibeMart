# Railway Deployment Guide for VibeMart

This guide will help you deploy your VibeMart Django project to Railway.app via GitHub.

## Prerequisites

1. A GitHub account
2. A Railway account (sign up at https://railway.app)
3. Your project pushed to a GitHub repository

## Deployment Steps

### 1. Prepare Your Repository

Your project is now ready for deployment! The following files have been configured:

- `requirements.txt` - Updated with production dependencies
- `railway.toml` - Railway configuration file
- `runtime.txt` - Python version specification
- `.gitignore` - Excludes sensitive files
- `settings.py` - Production-ready Django settings
- `.env.example` - Environment variables template

### 2. Push to GitHub

Make sure all your changes are committed and pushed to GitHub:

```bash
git add .
git commit -m "Configure project for Railway deployment"
git push origin main
```

### 3. Deploy on Railway

1. Go to [Railway.app](https://railway.app) and log in
2. Click "New Project"
3. Choose "Deploy from GitHub repo"
4. Select your repository
5. Railway will automatically detect it's a Python project and start building

### 4. Configure Environment Variables

In your Railway project dashboard:

1. Go to the "Variables" tab
2. Add the following environment variables:

**Required:**
- `SECRET_KEY` - Generate a new secret key for production
- `DEBUG` - Set to `False`

**Optional:**
- `CUSTOM_DOMAIN` - If you have a custom domain
- `DJANGO_LOG_LEVEL` - Set to `INFO` or `ERROR`

**Automatic:**
Railway automatically provides database variables when you add a PostgreSQL service.

### 5. Add PostgreSQL Database

1. In your Railway project, click "New Service"
2. Choose "Database" → "PostgreSQL"
3. Railway will automatically set up the database and provide connection variables

### 6. Generate a New Secret Key

For production, generate a new secret key:

```python
python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"
```

Use this value for the `SECRET_KEY` environment variable.

### 7. Custom Domain (Optional)

If you want to use a custom domain:

1. In Railway project settings, go to "Domains"
2. Add your custom domain
3. Set the `CUSTOM_DOMAIN` environment variable to your domain

## Project Structure

```
vibemart/
├── railway.toml          # Railway configuration
├── runtime.txt           # Python version
├── requirements.txt      # Dependencies
├── .gitignore           # Git ignore rules
├── .env.example         # Environment variables template
├── manage.py            # Django management
├── vibemart/
│   ├── settings.py      # Production-ready settings
│   └── ...
├── accounts/            # User accounts app
├── shop/               # Shop functionality
├── dashboard/          # Dashboard app
├── templates/          # HTML templates
└── static/            # Static files
```

## Features Configured

- ✅ Production-ready Django settings
- ✅ PostgreSQL database support
- ✅ Static files handling with WhiteNoise
- ✅ Environment variables support
- ✅ Security settings for production
- ✅ Automatic migrations on deployment
- ✅ Gunicorn WSGI server
- ✅ Logging configuration

## Troubleshooting

### Common Issues

1. **Build fails**: Check the build logs in Railway dashboard
2. **Static files not loading**: Ensure `collectstatic` runs during deployment
3. **Database connection errors**: Verify PostgreSQL service is added
4. **500 errors**: Check application logs in Railway dashboard

### Logs

View application logs in Railway:
1. Go to your project dashboard
2. Click on your service
3. Go to "Logs" tab

## Local Development

For local development:

1. Copy `.env.example` to `.env`
2. Update the values in `.env` for local development
3. Use SQLite database (default for `DEBUG=True`)

## Support

If you encounter issues:
1. Check Railway documentation: https://docs.railway.app
2. Review Django deployment guide: https://docs.djangoproject.com/en/5.2/howto/deployment/
3. Check project logs in Railway dashboard 