This is the example site for github.com/mreider/krems. You should clone it according to the instructions at the other repo:

## How It Works: Get Started with the Example Site
The easiest way to understand Krems is to explore the example site.

**Clone the Example Site:**
```bash
git clone https://github.com/mreider/krems-example.git
cd krems-example
```
Explore the Structure: Look at the `config.yaml` file, the markdown files (`.md`), and how content is organized. This will give you a feel for how Krems projects are structured.

### 3. Build It Locally
To build the site from the markdown files into static HTML:
```bash
krems --build
```
This command will generate the website into a `docs/` folder.

### 4. Run It Locally
To preview your site locally after building it:
```bash
krems --run
```
This will start a local web server, typically at `http://localhost:8080`. The `krems --run` command automatically rebuilds the site using settings suitable for local development (like `devPath: "/"` in your `config.yaml`).

### 5. Deploy Your Own Site with GitHub Pages
You can easily host your Krems site for free using GitHub Pages. The `krems-example` repository includes a GitHub Actions workflow that automates building and deploying your site.

**Create Your Repository on GitHub:** Go to GitHub and create a new, empty repository (e.g., `yourusername/my-new-blog`).

**Clone the Example and Set Your Remote:**
```bash
# Clone the example site into a temporary directory
git clone https://github.com/mreider/krems-example.git my-blog-temp
cd my-blog-temp

# Change the remote URL to point to *your* new GitHub repository
git remote set-url origin https://github.com/yourusername/my-new-blog.git # Replace with your repo URL

# Push the example site's code to your new repository
# (Use 'main' or your repository's default branch name)
git push -u origin main
```
**GitHub Actions Workflow:** The `krems-example` site includes a GitHub Actions workflow file (in `.github/workflows/`). When you push code to your repository's `main` branch, this workflow automates the deployment:

*   It automatically builds your Krems site (the workflow uses an internal build directory, typically `public/`, for this).
*   It then deploys the built site from this internal directory to a special `gh-pages` branch in your repository.

Note: This automated workflow process is distinct from running `krems --build` locally, which outputs to the `docs/` directory for local preview. The `docs/` directory is intended for local development and is ignored by Git.

**Configure GitHub Pages:**

1.  In your GitHub repository, go to "Settings" > "Pages".
2.  Under "Build and deployment", for "Source", select "Deploy from a branch".
3.  For "Branch", choose `gh-pages` and ensure the folder is set to `/ (root)`. Click "Save".

Your site will typically be available at `https://yourusername.github.io/my-new-blog/`.

### 6. Configure Your Site
After setting up your repository, you'll need to customize the configuration:

**Edit `config.yaml`:** Open the `config.yaml` file in your repository.

*   `website.url`: Change this to your site's URL.
    *   For a GitHub Pages site like `https://yourusername.github.io/my-new-blog/`, set it to this URL.
    *   If using a custom domain (e.g., `https://www.myawesomeblog.com`), set it to your custom domain.
*   `website.name`: Set your desired site name (appears in the navigation bar).
*   `website.basePath`: This is important for links to work correctly.
    *   If your site is at `https://yourusername.github.io/my-new-blog/`, set `basePath: "/my-new-blog/"`.
    *   If your repository is named `yourusername.github.io` and you want the site at `https://yourusername.github.io/`, set `basePath: "/"`.
    *   If using a custom domain pointing to the root, set `basePath: "/"`.
*   `website.devPath`: For local development with `krems --run` or `krems --build` (locally), you'll typically want `devPath: "/"`. This is usually pre-configured in the example.
*   Update the `menu` section to reflect your site's structure.

**Custom Domain (CNAME):** If you want to use a custom domain (e.g., `www.myawesomeblog.com`):

1.  First, configure your custom domain in your repository's "Settings" > "Pages" section on GitHub.
2.  Then, simply set the `website.url` in your `config.yaml` to your full custom domain URL (e.g., `https://www.myawesomeblog.com`). Krems will automatically generate the necessary `CNAME` file during the build process.

That's it! You now have a simple, markdown-powered blog or website running with Krems.
