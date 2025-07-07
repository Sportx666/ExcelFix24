# ExcelFix24

This site is built with [Hugo](https://gohugo.io/) using a small custom theme located in `themes/excelfix`.

## Building
Only Hugo is required to build or test the site locally. Use `hugo server` to run a local development server or `hugo --minify` to generate the `public` output directory.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Deployment
The site is built and deployed automatically using [GitHub Actions](.github/workflows/hugo-gh-pages.yml). The generated content in `public` is published to the `gh-pages` branch. Configure the repository's GitHub Pages settings to serve the site from this branch.

> **Note**
> 
> - GitHub Pages must deploy from the `gh-pages` branch. Navigate to **Settings** → **Pages** in this repository and choose **Deploy from branch**, selecting `gh-pages` and `/` as the source.
> - If you serve from the repository root, GitHub will display your `README.md` instead of the built site unless an empty `.nojekyll` file is present.

## Styling
All site styles are compiled into `static/assets/css/custom.css`. Previous SCSS
sources have been removed because the build does not use Hugo Pipes. Edit the
`custom.css` file directly if you need to adjust the design.
