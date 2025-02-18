# 11ty Personal Blog

Welcome to the 11ty (Eleventy) version 3 project! This README provides an overview of the project structure, setup, and key features. Follow the instructions below to get started and customize the site as needed.

---

## Table of Contents

- [11ty Personal Blog](#11ty-personal-blog)
  - [Table of Contents](#table-of-contents)
  - [About 11ty](#about-11ty)
  - [Features](#features)
  - [Requirements](#requirements)
  - [Installation](#installation)
  - [Project Structure](#project-structure)
  - [Usage](#usage)
    - [Development](#development)
    - [Build](#build)
    - [Serve](#serve)
  - [Customization](#customization)
    - [Layouts](#layouts)
    - [Content](#content)
    - [Global Data](#global-data)
    - [Styles](#styles)
  - [Deployment](#deployment)
    - [Popular Deployment Options](#popular-deployment-options)
  - [Contributing](#contributing)
  - [License](#license)

---

## About 11ty

Eleventy (11ty) is a simple, flexible, and fast static site generator. It allows developers to build modern websites using templating languages like Nunjucks, Liquid, Markdown, and more.

Learn more about 11ty on the [official website](https://www.11ty.dev/).

---

## Features

- **Modern Development Workflow**: Uses 11ty version 3 for optimal performance and new features.
- **Flexible Templating**: Supports multiple template engines.
- **Markdown-First**: Create content easily with Markdown.
- **Customizable Layouts**: Organize your site with reusable layouts.
- **Static Asset Management**: Optimize and manage CSS, JavaScript, and images.

---

## Requirements

- **Node.js**: Version 16 or later
- **npm** or **yarn**: For package management

---

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/hieulvVn/eleventy-blog.git
   cd eleventy-blog
   ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. Run the development server:

   ```bash
   npm start
   ```

4. Build the site for production:

   ```bash
   npm run build
   ```

---

## Project Structure

```
.
├── _data/         			# Global data files
├── _includes/     			# Layouts, partials, and components
├── _config/     				# Setting filter,...
├── public/        			# Static assets (CSS, JS, images)
│──	content/						# source content overall
│		├── blog/         	# Blog posts (Markdown files)
│		├── feed/         	# Feed RSS setting
├── eleventy.config.js  # Eleventy configuration file
├── package.json        # Project metadata and scripts
├── README.md           # Project documentation
└── .gitignore          # Files to ignore in Git
```

---

## Usage

### Development

- Start the development server with live reload:
  ```bash
  npm start
  ```

### Build

- Generate a production-ready version of the site:
  ```bash
  npm run build
  ```

### Serve

- Preview the production build:
  ```bash
  npm run serve
  ```

---

## Customization

### Layouts

Layouts are stored in the `_includes/` directory. Update or create new layouts as needed.

### Content

Content files (e.g., blog posts) are located in the `content/blogs/` directory. Add new Markdown files for additional posts.

### Global Data

Global data files are stored in the `_data/` directory. Update these files to modify site-wide settings.

### Styles

Custom CSS files are located in the `public/` directory. Update or add new styles to change the site's appearance.

---

## Deployment

The production build generates static files in the `_site/` directory. Deploy this folder to your preferred hosting service.

### Popular Deployment Options

- **Netlify**:

  - Connect your repository to Netlify and set the build command to:
    ```bash
    npm run build
    ```
  - Set the publish directory to `_site`.

- **Vercel**:

  - Deploy with Vercel's CLI or dashboard.
  - Build command: `npm run build`
  - Output directory: `_site`

- **GitHub Pages**:
  - Use GitHub Actions to automate deployment.

---

## Contributing

Contributions are welcome! If you have suggestions or improvements, feel free to submit a pull request or open an issue.

---

## License

This project is licensed under the [MIT License](LICENSE).
