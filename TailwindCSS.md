Install tailwind using npm

npm install tailwindcss --save-dev
or using yarn

yarn add tailwindcss --dev
Create a Tailwind.js configuration file

Type the following to create a tailwind.js configuration file

./node_modules/.bin/tailwind init tailwind.js
Configuring PostCSS

Create a postcss.config.js file touch postcss.config.js

Then proceed to configure Postcss to process tailwind, Do that by adding the following code to your postcss.config.js file

module.exports = {
	"plugins": [
 		require('tailwindcss')('tailwind.js'),
 		require('autoprefixer')(),
	]
}

postcss.config.js file
Remove all tailwind configurations from package.json

Delete the following lines of code from thepackage.json file

    "postcss": {
    "plugins": {
      "autoprefixer": {}
    }
  },
  
Create a CSS file

Navigate to src/assets/cssand create a new tailwind.css file in yourcssfolder, the add the following

@tailwind base;@tailwind components;@tailwind utilities;

Import Tailwind into your vue app

Open your main.js file and add :

import '@/assets/css/tailwind.css'