# Is It #000000?

A fun game where you test your ability to distinguish true black (#000000) from very dark grays.

## Features

- 10 rounds of color guessing
- Score tracking
- Mobile-responsive design
- Clean, modern UI

## Local Development

1. Clone the repository
2. Install dependencies:
   ```bash
   npm install
   ```
3. Start the development server:
   ```bash
   npm run dev
   ```

## Deployment to Cloudflare Pages

1. Push your code to a GitHub/GitLab repository
2. Go to [Cloudflare Pages](https://pages.cloudflare.com/)
3. Click on "Create a project"
4. Select your repository
5. Configure the build settings:
   - Framework preset: `Vite`
   - Build command: `npm run build`
   - Build output directory: `dist`
   - Root directory: `/`
6. Click "Save and Deploy"

## Environment Variables

No environment variables are required for this project.

## License

MIT
