{

​    "terminal.integrated.cwd": "${workspaceFolder}",

​    "terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe",

​    "editor.fontFamily": "Hack, Consolas, 'Courier New', monospace",

​    "[html]": {

​        "editor.tabSize": 2

​    },

​    "[css]": {

​        "editor.tabSize": 2

​    },



​    "[django-html]": {

​        "editor.tabSize": 2

​    },



​    

​    "beautify.language": {

​        "js": {

​        "type": ["javascript", "json"],

​        "filename": [".jshintrc", ".jsbeautifyrc"]

​        // "ext": ["js", "json"]

​        // ^^ to set extensions to be beautified using the javascript beautifier

​        },

​        "css": ["css", "scss"],

​        "html": ["htm", "html", "django-html"],

​        // ^^ providing just an array sets the VS Code file type

​    },

​      



​    // django

​    "files.associations": {

​        "**/*.html": "html",

​        "**/templates/**/*.html": "django-html",

​        "**/templates/**/*": "django-txt",

​        "**/requirements{/**,*}.{txt,in}": "pip-requirements"

​    },

​    "emmet.includeLanguages": {

​        "django-html": "html"

​    },

​    "workbench.iconTheme": "material-icon-theme",

}