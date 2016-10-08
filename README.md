This is my blog. I am using [Harp.js](https://harpjs.com/) for static site generation.

If you want to fork / build on top of this, you just need to install harp per their instructions: `npm install -g harp`. One caveat -- it seems that harp does not play nicely with `node_modules` at the time of this writing. (See [this issue](https://github.com/sintaxi/harp/pull/312) for more details.) I originally had a package.json, but it was breaking all the things, so I'm installing harp globally now and trying not to curl up into the fetal position.

Confirmed working with Harp.js 0.20.3.

Feel free to open a ticket if you try to run this and have any trouble!
