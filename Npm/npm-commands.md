
# Npm Commands 

- [Get info](#get-info)

- [initialize the project](#initialize-the-project)

- [Managing packages](#managing-packages)

- [Run scripts](#run-scripts)

- [Publish packages](#publish-packages)

</br>



# Get info

## getting the version of npm 
- `npm -v (or --version)`

## get the npm documentation 
- `npm help` *or* `npm`

- `npm [command] -h`

  *get a short documentation about that specific command*

- `npm help [command]`

  *get the full documentation of the specific command*
  
## Find root folder
- `npm root -g`

## Listing packages
- `npm list `  *or* ` npm ls`

  *list all the packages installed each with their dependencies,  if with `-g` flag will list the global packages*

- `npm list --depth=[max-depth]` *or* ` npm list --depth [max-depth]`

  *will list all the packages with the defined dependencies level e.g.* `npm list --depth 0` 

- `npm list --long=true` 

  *will list the packages with a sort of description about them*

- `npm list --json `

  *list the packages in json format* 

- `npm list --dev `

  *list all the devDependencies* 

- `npm list --prod `

  *list all the non devDependencies* 
  
## get info about a package 

*can specify '-g' to make npm look at global packages*

- `npm show [package-name]` 

    *will show some kind of generic description and options avaible.*    *e.g*.`   npm show express`

- `npm show [package-name] [option]`  
  
     *will show specific information based on the option provided about the package*
     
      - `npm show lodash version`  *get the lastest version of lodash.*
      - `npm show lodash versions`  *get an array of all the version of lodash.*
      - `npm show express dependencies`  *get all the dependencies which express depends on.*

## get info about the vesions of the packages that need to be updated

*either global or local ( it depends on how are installed in package.json, if with '~, ^ or =' )*

- `npm outdated `

  *add `-g` to make npm look for global packagees*

## Additional info about the project and packages

- `npm info`

  *get info about the project (in the current directory)*

- `npm repo [package-name]`

  *direct to the gitHub browser page of the package* e.g.* `npm repo express`

</br>


# initialize the project 

## Create package json
- `npm init`
- `npm init -y (or --yes)` *skip all the questions*

## Set defaults properties 

*set default properties of the project to package.json*

- `npm config set [property][value]` *or just* `npm set [property][value] `

  *accept the property name and the new value to set (string)*

  - `npm set init-license "MIT"`
  - `npm set init-description "lorem ipsum ..."`
  - `npm set init-name "project-something"`
  - `npm set init-author-name "mario guzzman"`

## Get defaults

*get properties of package.json based on the name provided*

- `npm get [property]`

  *e.g.*  `npm get init-license`

## Remove defaults
- `npm delete [property]`

  *e.g.*  `npm delete init-license`

## Move to another folder
- `npm install`
- `npm install --production`

</br>


# Managing packages 

## Installing local packages

*install packages in the current folder, **will automatically be saved as dependencies ** in package.json.*

- `npm install [package-name]`     

   *e.g.*  `npm install lodash`

## install local packages as devDependencies 

*install packages and save them as devDependencies in package.json*

- `npm install [package-name] [package-name] --save-dev`

## Install global module

*install packages globally, use just when they **require the command line in order to work***

- `npm install -g [package-name]`

    *e.g.* `node install -g nodemon`

## Install certain versions
- `npm install [package-name]@4.17.3  ` 

  *will install exactly this vesrion.  e.g.*  `npm install lodash@4.17.3  `

- `npm install [package-name]@4` 

  *will install the lastest minor version.*

- `npm install [package-name]@4.17`

   *will intall  the lastest patch version.*

- `npm install [package-name]@lastest` 

- *install the lastest major version, npm usually does it automatically but who knows...*

## Removing modules
- `npm remove [package-name]`

  *remove installed package and delete dependency from package.json*

- `npm remove [package-name] --save-dev`  

  *remove from devDependencies*

- `npm remove -g [package-name]` 

  *Remove global packages* *e.g.* `node remove -g nodemon`

## Update

- `npm update`

  *will update all the dependencies, add `-g` to update the global dependencies* 

- `npm update [package-name]`

  *will update a specific dependency, add `-g` to npm look for a global dependency

- `npm update -g npm` 

  *update npm with npm itself*

## Install local package 

- `npm install [path-to-folder]`

  *e.g.* `npm install ./my-package `

</br>

# Run scripts 

## run any custom command under 'scripts' in package.json (in the main directory)
- `npm run [command]` 
- `npm run check` (usually in package.json will be "check": "eslint main.js" -> this won't work cause .eslint conf file is not configured yet, for this you need npx to access the command eslint)

## run special character commads under 'scripts', full list using 'npm help npm-scripts'
- `run start` (in package.json declared as "start": "node main.js")
- `run test`  (declared usually as "test": "jest" -> third party package for testing)
- `npm pretest` (automatically run before npm start testing, usually -> "pretest": "node -e 'console.log(\"starting testing\")'" or can run a entire new file for pretesting)
- `npm posttest` (automatically run after the test is done, usually -> "posttest": "node -e 'console.log(\"done testing\")'")

## Npx: run commands not declared in scripts and bound to local packages (accessible only via npm)
- `npx jest` (equivalent to npm test)
- `npx eslint --init` (this is needed to create a .eslint confiuration file before checking, after this *you can use* either- `npm run check` or `npx eslint main.js` )

</br>


# Publish packages

## login the account 

*login the shell to an existing Npm account*

- `npm login` 

## publish a package

- `npm publish` 

  *will publish the package from the current directory*

## update the package 

*update the version of the package in Npm*

- `npm version [version-type]`

  *will update the version increasing by one in package.json, also will automatically commit the version to the git repository (commits the changes of package.json).*

  Can be updated either the major, minor or patch version :

  - `npm version major`
  - `npm version minor`
  - `npm version patch`

- `npm plubish`

  *publish the changes to npm*

## publish beta version 

*`beta` or `alpha` are just convenstions, can be used any name.*

- Add the version in package.json: `"version": "[version]-beta.[sub-version]"`

  *Needs to be setted manually in the file.  e.g.*``"version": "1.0.1-beta.0"``

- `npm  publish --tag beta` 

  *will add a new version with the tag provided, complitely separeted from the latest version. If a user want to install the beta version needs to probide the tag in the install command.  e.g.*`npm i express@beta`

  
