# VtubeVerynice

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 10.0.2.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).

## Notes

### 'Manually' Publishing to GitHub Pages
- deployable code generated in `dist/project_name1` by default
  - needs to be generated in `docs` folder, under the app folder
    - change `angular.json`: `"outputPath": "docs/"`
- build with base URL to `https://username.github.io/respositoryname`   
  - `ng build --prod --baseHref=”https://adiguno.github.io/v_v/”`

### 'Automagically" Publishing to GitHub Pages
- `ng add angular-cli-ghpages`
- `ng deploy --base-href=/v_v/` project name

### Loading images
- use `assets/{resource}`, no slash before 'assets'

### Adding Bottstrap
  1. using npm `npm install bootstrap`
     - updated `package.json`
     - installed in `node_modules/bootstrap`
     - jQuery also needs to be installed `npm install jquery`
  2. add bootstrap to `angular.json`
     - node_modules/bootstrap/dist/css/bootstrap.css in the projects->architect->build->styles array,  
     - node_modules/bootstrap/dist/js/bootstrap.js in the projects->architect->build->scripts array,  
     - node_modules/bootstrap/dist/js/bootstrap.js in the projects->architect->build->scripts array,
     - also need to add the jquery js lib file

### Quickly restructure JSON
 - `shift + option + f`