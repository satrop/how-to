<h1>Simple HTML with GH-Pages Setup</h1>

In case you want to set up a super simple HTML page with SCSS and dont want to use plugins.

### Notes

-   All terminal command are run in VSCodes built in terminal

---

## Setup Your Project

Nothing fancy. All files will go in the src folder. And be sure to label your SASS folder 'SASS', with an 'A'. You can use SCSS but you'll have to update the `package.json` to match.

```bash
├── Project-Name
│   ├── src
│   │   ├── assets
│   │   ├── js
│   │   ├── images
│   │   ├── sass
│   │   ├── index.html
└── package.json
```

Now jump into your `package.json` file and copy past the following:

<b>Note:</b> If using Windows you'll need to change:
`"watch:html": "onchange 'src/*.html' -- npm run copy:html",` to:
`"watch:html": "onchange \"src/*.html\" -- npm run copy:html",`

Windows doesn't like the single quotes.

```sh
{
	"name": "Project-Name",
	"version": "0.1.0",
	"description": "Add your own description...",
	"main": "public/index.html",
	"homepage": "/project-name/",
	"scripts": {
		"build:sass": "sass  --no-source-map src/sass:dist/css",
		"copy:html": "copyfiles -u 1 ./src/*.html dist",
		"copy": "npm-run-all --parallel copy:*",
		"watch:html": "onchange 'src/*.html' -- npm run copy:html",
		"watch:sass": "sass  --no-source-map --watch src/sass:dist/css",
		"watch": "npm-run-all --parallel watch:*",
		"serve": "browser-sync start --server dist --files dist",
		"start": "npm-run-all copy --parallel watch serve",
		"build": "npm-run-all copy:html dist:*",
		"postbuild": "postcss dist/css/*.css, -u autoprefixer cssnano -r --no-map",
		"deploy": "gh-pages -d dist"
	},
	"dependencies": {
		"autoprefixer": "^10.4.2",
		"browser-sync": "^2.27.7",
		"copyfiles": "^2.4.1",
		"cssnano": "^5.0.17",
		"npm-run-all": "^4.1.5",
		"onchange": "^7.1.0",
		"postcss-cli": "^9.1.0",
		"sass": "^1.49.8"
	},
	"devDependencies": {
		"gh-pages": "^5.0.0"
	}
}
```

Be sure to change `"name": "Project-Name",` / `"homepage": "/project-name/",` to your project name.

---

## Install Dependencies

1. In terminal (within VSCode) run:

```sh
npm i
```

2. Run:

```sh
npm start
```

This'll build the project, start watching your SASS/SCSS folder and fire up a live server.

---

## Initialize Git

1. Run:

```sh
git init
```

In the `.gitignore` file that was created you can add these if you want:

```sh
# Logs
logs
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*
pnpm-debug.log*
lerna-debug.log*

node_modules
dist
dist-ssr
*.local

# Editor directories and files
.vscode/*
!.vscode/extensions.json
.idea
.DS_Store
*.suo
*.ntvs*
*.njsproj
*.sln
*.sw?
```

2. Run

```sh
git add . && git commit -m "Init push"
```

3. Go to [GitHub](https://github.com/) and create new repo and call it what you like.
4. Follow the "<b>…or push an existing repository from the command line</b>" instructions. Copy the instruction <b>from GitHub</b> because it will auto populate "your-account-name" and "project-name" and past that into your VSCodes terminal.

### Example:

```sh
git remote add origin https://github.com/{your-account-name}/{project-name}.git {<-- Change "your-account-name" and "project-name" }
git branch -M main
git push -u origin main
```

Now back to your project:

1. Run:

```sh
npm run deploy
```

This command pushes your project to gh-pages.
