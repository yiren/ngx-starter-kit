DIY Playbook
============

Do-it-yourself step-by-step instructions to create this project structure from scratch.


### Prerequisites  
| Software                      | Version  | Optional |  
|-------------------------------|----------|----------| 
| Node                          | v9.4.0   |          | 
| Angular CLI                   | v1.6.5   |          | 
| @nrwl/schematics              | v0.7.3   |          | 


### Install Prerequisites
```bash
# install or Update Node with brew or NVM
brew update
brew install node
#brew upgrade node
```

#### Install Global Packages
```bash
npm remove -g @nrwl/schematics
npm install -g @nrwl/schematics
npm install -g @angular/cli

# verify globally installed packages
npm list -g --depth=0
# set scss as default css processor
ng set defaults.styleExt scss
```

### Scaffold Project
> steps below are for setting up a new project from the scratch.

#### Create Workspace
```bash
create-nx-workspace nx-starter-kit
cd nx-starter-kit
npm install
```

#### Dependencies
> adding 3rd party modules/libs
```bash
cd nx-starter-kit
npm i @angular/flex-layout @angular/material @angular/cdk @angular/material-moment-adapter hammerjs web-animations-js  \
ngx-perfect-scrollbar screenfull angular2-moment \
@swimlane/ngx-datatable @swimlane/ngx-charts angular-in-memory-web-api 
 
npm i -D loaders.css @types/hammerjs standard-version

#  temp workaround
npm i -D @angular/http

npm i d3
npm i nvd3
npm i -D @types/nvd3
npm i -D @types/d3
```

#### Generate Artifacts
> Add  `--dry-run` option to following commands to see which artifacts will be created, without actually creating them.
```bash
# generate default app
ng g app default --routing --style=scss --service-worker

# add `core` module to `default` app
ng g module core --app=default --module=app
# add shared services for `core` Module
ng g service core/services/InMemoryData --app=default --module=core --spec=false
ng g service core/services/PageTitle/PageTitle --app=default --module=core
ng g service core/services/serviceWorker/serviceWorker --app=default --module=core --dry-run

# generate `Lazy-loaded Feature Modules`
ng g lib home           --routing --lazy --parent-module=apps/default/src/app/app.module.ts
ng g lib dashboard      --routing --lazy --parent-module=apps/default/src/app/app.module.ts
ng g lib admin          --routing --lazy --parent-module=apps/default/src/app/app.module.ts 
ng g lib experiments    --routing --lazy --parent-module=apps/default/src/app/app.module.ts 
ng g lib NotFound       --routing --lazy --parent-module=apps/default/src/app/app.module.ts
ng g lib widgets        --routing --lazy --parent-module=libs/dashboard/src/dashboard.module.ts
ng g lib crud           --routing --lazy --parent-module=libs/dashboard/src/dashboard.module.ts

ng g lib material --spec=false --dry-run
ng g lib animations --nomodule --dry-run 
ng g lib Tree --nomodule --dry-run 

ng g lib shared # add `shared` module which will encapsulate angular and 3rd party modules, needed for all `Lazy-loaded Feature Modules`  

# generate containers, components for `shared` Module
ng g service services/entity/entity --app=shared --module=shared
ng g directive directives/min  --app=shared --module=shared --export=true
ng g component components/entityTable --app=shared --module=shared --export=true
ng g component containers/entity --app=shared --module=shared --skip-import
ng g component containers/entityForm  --app=shared --module=shared --skip-import

# generate containers for `NotFound` Module
ng g component containers/NotFound --app=not-found


### generate `Reusable lib Modules`

# generate components for `AppConfirm` Module
ng g lib AppConfirmq --dry-run
ng g component AppConfirm --app=app-confirm  --flat  --dry-run
ng g service AppConfirm --app=app-confirm --module=app-confirm --spec=false --dry-run

# generate components for `fullscreen` Module
ng g lib Fullscreen
ng g component fullscreen --app=fullscreen --flat --dry-run

# generate components for `Breadcrumbs` Module
ng g lib Breadcrumbs
ng g component breadcrumbs --app=breadcrumbs --flat --dry-run
ng g service  breadcrumbs --app=breadcrumbs --module=breadcrumbs --dry-run

# generate components for `ScrollToTop` Module
ng g lib ScrollToTop
ng g component ScrollToTop --app=scroll-to-top --flat --dry-run

# generate components, services for `ThemePicker` Module
ng g lib ThemePicker  
ng g component ThemePicker --app=theme-picker --flat --dry-run
ng g service  ThemeStorage --app=theme-picker --module=theme-picker --dry-run
ng g service  StyleManager --app=theme-picker --module=theme-picker --dry-run

# generate components for `Quickpanel` Module
ng g lib Quickpanel
ng g component Quickpanel --app=quickpanel --flat --dry-run

# generate components for `LoadingOverlay` Module
ng g lib LoadingOverlay
ng g component LoadingOverlay --app=loading-overlay --flat --dry-run

# generate components for `svgViewer` Module
ng g lib svgViewer
ng g component svgViewer --app=svg-viewer --flat --dry-run 

# generate components for `toolbar` Module
ng g lib toolbar --dry-run 
ng g component toolbar --app=toolbar --flat --dry-run 
ng g component components/search --app=toolbar  --dry-run 
ng g component components/searchBar --app=toolbar
ng g component components/Notifications --app=toolbar
ng g component components/UserMenu --app=toolbar
ng g directive components/ClickOutside/ClickOutside  --app=toolbar --dry-run 

# generate components for `sidenav` Module
ng g lib sidenav --dry-run 
ng g component sidenav --app=sidenav --flat --dry-run 
ng g component components/sidenavItem --app=sidenav  --dry-run 
ng g service services/navigation/navigation --app=sidenav --module=sidenav --dry-run 
ng g directive  IconSidenav --app=sidenav --module=sidenav --dry-run 

# generate containers, components for `home` Module
ng g component components/header --app=home
ng g component containers/homeLayout --app=home
ng g component containers/landing --app=home
ng g component containers/blog --app=home
ng g component containers/about --app=home

# generate containers, components, services for `dashboard` Module
ng g component components/header --app=dashboard 
ng g component components/footer --app=dashboard
ng g component containers/dashboardLayout --app=dashboard --dry-run
ng g component containers/accounts --app=dashboard
ng g service services/account/account --app=dashboard --module=dashboard
 



ng g component components/searchBar --app=dashboard
ng g component components/sideBar --app=dashboard
ng g component components/sideMenuItem --app=dashboard
ng g component components/sideMenu --app=dashboard
ng g component components/toolBarNotification --app=dashboard
ng g component components/toolBar --app=dashboard
ng g component components/userMenu --app=dashboard


# generate containers, components for `widgets` Module
ng g component containers/wizdash --app=widgets --dry-run

# generate containers, components for `crud` Module
ng g component containers/accounts --app=crud --module=crud --dry-run

# generate containers, components for `admin` Module
ng g component containers/adminLayout --app=admin --dry-run
ng g component containers/overview --app=admin --dry-run
ng g component components/rainbow --app=admin --dry-run

# generate containers, components for `experiments` Module
ng g component containers/experimentsLayout --app=experiments --dry-run
ng g component containers/experiments --app=experiments --dry-run
ng g component components/hammerCard --app=experiments --dry-run
ng g directive components/Hammertime/Hammertime --app=experiments --dry-run



# scaffolding ngrx for root module i.e., app.module.ts
ng g ngrx app --app=default --module=apps/default/src/app/app.module.ts  --only-empty-root
# add `account` state for `dashboard` Feature Module
ng g ngrx account --directory=state/account --app=dashboard --module=libs/dashboard/src/dashboard.module.ts
```

### Install
```bash
npm install
cp .env.example .env
```
### Test
```bash
ng test --browser=ChromeHeadless
```

### Build
```bash
# build themes
# build project 
ng build --prod -oh=media
ng build -e mock -oh=media
```
### Run
```bash
# run mock mode
ng s -e mock --extract-css --preserve-symlinks -o
# ES2015 support: Set tsconfig.json target value as "es2015" and  use --aot 
ng s -e mock --extract-css --preserve-symlinks --aot -o
# run prod mode
ng s -e prod
```

### Serve from dist
> use this to test service-workers
```bash
# 1st terminal - Start the build
ng build --watch
# 2nd terminal - Start the web server
npx lite-server --baseDir="dist"
```

### Release
```bash
npx standard-version
"release": "standard-version && git push — follow-tags origin master && npm publish"
```
### Demo Deploy
```bash
ng build --prod -e mock --output-path docs --base-href nx-starter-kit
# Make a copy of docs/index.html and name it docs/404.html
```

### Production build and deployment
The prod image serves the minified app (sources compiles with a minimal set of dependencies), via an Nginx server. 
It is self-contained, and can therefore be pushed to a Docker registry to be deployed somewhere else easily.

To start the container, use:
```bash
$ docker-compose -f docker-compose.prod.yml up -d   # optional: --build, see below
```

Now open your browser at http://localhost:5555