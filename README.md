# Frontend workflow

## Wat
Een combinatie van verschillende tools en files die ervoor zorgen dat we projecten snel kunnen opzetten en makkelijk kunen onderhouden.
- versies van dependencies vastleggen
- build proces vastleggen (scss, js, ...)

## Systeem 

### 1. Ruby
- gebruik [RVM](https://rvm.io/) om makkelijk te updaten en te switchen tussen ruby versies.
- of [RBenv](http://rbenv.org/)
- **@TODO**: welke is de beste manier?

### 2. Node.js
- [http://nodejs.org/](http://nodejs.org/)
- nodig om Bower en Gulp te draaien

### 3. Bundler, Bower, Gulp en EditorConfig als global dependencies
- [http://bundler.io/](http://bundler.io/) => `gem install bundler`
- [http://bower.io/](http://bower.io/) => `npm install -g bower`
- [http://gulpjs.com/](http://gulpjs.com/) => `npm install -g gulp` 
- [http://editorconfig.org/](http://editorconfig.org/)

## Dependencies

### 1. Editorconfig
- [http://editorconfig.org/](http://editorconfig.org/)
- instellingen voor tabs, spaties, ... per project zodat we **'die'** discussie nooit meer moeten voeren.
- worden per filetype bijgehouden in een **'.editorconfig'** file
- er zijn [plugins](http://editorconfig.org/#download) beschikbaar voor de meest courante editors 

### 2. Bundler
- werkt met een **'Gemfile'**
- `bundle install` laadt alle correcte gems in. (vb Sass, Compass, Jekyll, Capistrano, ...)
- bundler switched automatisch tussen de gems per project afhankelijk van de gegenereerde **'gemfile.lock'**
- resource voor de gem versies => [https://rubygems.org/](https://rubygems.org/)

### 3. Bower
- om project afhankelijke plugins/dependencies te beheren en makkelijk bij te werken (vb. Jquery, html5shiv, respond, ...)
- `bower install` laadt alle dependencies in die in de **'bower.json'** staan
- optioneel kan je met een **'.bowerrc'** de locatie van deze bestanden definiëren. Standaard is dit **'bower_components'**.
- `bower search *package-name*` om de juiste package te vinden
- `bower list` toont je de geïnstalleerde packages en hun huidige versies + de nieuwe versie als deze er is
- `bower install *package-name* --save` installeert een package en slaat deze op in de **'bower.json'**
- Zet ook de **'bower_components map'** in je gitignore. Zo hoef je dependencies niet te uploaden. Tenzij je github pages gebruikt of als je een project deployed. 
- **@TODO**: `bower install` in het deployment process steken?

### 4. Gulp
- dit is een task runner die draait op [Node.js](http://nodejs.org/)
- deze werkt met plugins maar kan ook shell commando's uitvoeren en pure javascript
- de **'package.json'** definieert alle plugins op projectbasis
- `npm install` installeert alle plugins in je project in een map **'node_modules'** (belangrijk dat je deze in je .gitignore zet)
- de gulp plugins en taken zijn gedefineerd in de 'gulpfile.js'
- `gulp`  zal altijd de default taak starten
- zorg ervoor dat je **'gulpfile.js'** en **'package.json'*** in de root van je project staan
- [meer plugins](http://gulpjs.com/plugins/)
- plugin toevoegen => `npm install *plugin* --save-dev` (--save-dev past de **'package.json'** aan)
- plugins updaten => `npm update --save-dev` (--save-dev past de **'package.json'** aan)
- **@TODO**: is een deploy taak hier nuttig? We zouden hiervoor de default taak kunnen gebruiken. Zou ervoor zorgen dat we geen CSS en minified javascript meer pushen dus minder merge conflicts, etc. Alles wordt gegenereerd bij de deploy.

## Workflow
- `bundle install` & `npm install` & `bower install` bij het opzetten van een project
- `gulp scss` => compileert scss + runt autoprefixer + combineert media-queries + minify
- `gulp js` => combineert js files + uglify
- `gulp jekyll--build` => genereert jekyll site
- `gulp` => scss + js + jekyll--build
- `gulp watch` => server + watch & reload

## Andere ideeën voor de toekomst

### Gulp workflow uitbreiden:
- [SVG naar PNG conversie](https://www.npmjs.org/package/gulp-svg2png/)
- Google pagespeed:

```
gulp.task('pagespeed', pagespeed.bind(null, {
  // By default, we use the PageSpeed Insights
  // free (no API key) tier. You can use a Google
  // Developer API key if you have one. See
  // http://goo.gl/RkN0vE for info key: 'YOUR_API_KEY'
  url: 'https://example.com',
  strategy: 'mobile'
}));
```

- [JS hint](https://www.npmjs.org/package/gulp-jshint/)
- ...

### Projecten opzetten
[Yeoman](http://yeoman.io/) gebruiken om snel projecten op te zetten. Met yeoman kan je verschillende variaties van een boilerplate snel opzetten.

