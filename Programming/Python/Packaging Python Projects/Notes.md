# Packaging Python Projects
* \_\_init\_\_.py is required to import the directory as a package, and should be empty.

```
packaging_tutorial/
  └── src/
    └── example_package/
      ├── \_\_init\_\_.py
      └── example.py
```

## Creating the package files
```
packaging_tutorial/
├── LICENSE
├── pyproject.toml
├── README.md
├── setup.cfg
├── src/
│   └── example_package/
│       ├── __init__.py
│       └── example.py
└── tests/
```

### Creating a test directory
* tests/ is a placeholder for test files.

### Creating pyproject.toml
* pyproject.toml tells build tools (like pip and build) what is required to build your project.
```
[build-system]
requires = [
  "setuptools>=42",
  "wheel"
]
build-backend = "setuptools.build_meta"
```
* build-system.requires gives a list of packages that are needed to build your package.
  * Listing something here will only make it available during the build, not after it is installed.
* build-system.build-backend is the name of Python object that will be used to perform the build.

### Configuring metadata
* There are two types of metadata: static and dynamic.
  * Static metadata (setup.cfg): guaranteed to be the same every time.
  * Dynamic metadata (setup.py): possibly non-deterministic.A
* Static metadata (setup.cfg) should be preferred. Dynamic metadata (setup.py) should be used only as an escape hatch when absolutely necessary.

#### setup.cfg
* setup.cfg is the configuration file for setuptools.
* It tells setuptools about your package (such as the name and version) as well as which code files to include.
```
  [metadata]
  name = example-pkg-YOUR-USERNAME-HERE
  version = 0.0.1
  author = Example Author
  author_email = author@example.com
  description = A small example package
  long_description = file: README.md
  long_description_content_type = text/markdown
  url = https://github.com/pypa/sampleproject
  project_urls =
      Bug Tracker = https://github.com/pypa/sampleproject/issues
  classifiers =
      Programming Language :: Python :: 3
      License :: OSI Approved :: MIT License
      Operating System :: OS Independent

  [options]
  package_dir =
      = src
  packages = find:
  python_requires = >=3.6

  [options.packages.find]
  where = src
```
* **name:** distribution name of your package
  * This can be any name as long as it only contains letters, numbers, _ , and -. 
  * It also must not already be taken on pypi.org.
  * Be sure to update this with your username, as this ensures you won’t try to upload a package with the same name as one which already exists.
* **version:** package version
* **long_description:** detailed description of the package
  * This is shown on the package detail page on the Python Package Index.
  * In this case, the long description is loaded from README.md (which is a common pattern) using the file: directive.
* **long_description_content_type:** Tells the index what type of markup is used for the long description (example: Markdown)
* **url:** URL for the homepage of the project
* **project_url:** lets you list any number of extra links to show on PyPI. Generally this could be to documentation, issue trackers, etc.
* **classifiers:** Gives the index and pip some additional metadata about your package.
* In the options category, we have controls for setuptools itself:
  * **package_dir:** Mapping of package names and directories.
  * **package:** List of all Python import packages that should be included in the distribution package.
    * Instead of listing each package manually, we can use the find: directive to automatically discover all packages and subpackages and options.packages.find to specify the package_dir to use.
  * **python_requires:** Gives the versions of Python supported by your project.
    * Installers like pip will look back through older versions of packages until it finds one that has a matching Python version.

## Generating distribution archives
* These are archives that are uploaded to the Python Package Index and can be installed by pip.
* Now run this command from the same directory where pyproject.toml is located:
  ```sh
  python3 -m build
  ```
  * Once completed should generate two files in the dist directory:
    ```
    dist/
      example_package_YOUR_USERNAME_HERE-0.0.1-py3-none-any.whl
      example_package_YOUR_USERNAME_HERE-0.0.1.tar.gz
    ```
    * The tar.gz file is a source archive whereas the .whl file is a built distribution.
    * Newer pip versions preferentially install built distributions, but will fall back to source archives if needed.
    * You should always upload a source archive and provide built archives for the platforms your project is compatible with.

## Uploading the distribution archives
* The first thing you’ll need to do is register an account on TestPyPI, which is a separate instance of the package index intended for testing and experimentation.
* To register an account, go to https://test.pypi.org/account/register/ and complete the steps on that page.
* You will also need to verify your email address before you’re able to upload any packages.
* To securely upload your project, you’ll need a PyPI API token.
  * Create one at https://test.pypi.org/manage/account/#api-tokens, setting the “Scope” to “Entire account”.
  * Don’t close the page until you have copied and saved the token — you won’t see that token again.
* You can use **twine** to upload the distribution packages
  * Run Twine to upload all of the archives under dist:
  ```sh
  python3 -m twine upload --repository testpypi dist/*
  ```
  * You will be prompted for a username and password.
    * For the username, use __token__.
    * For the password, use the token value, including the pypi- prefix.

## Installing your newly uploaded package
* You can use pip to install your package and verify that it works.
```sh
python3 -m pip install --index-url https://test.pypi.org/simple/ --no-deps example-pkg-YOUR-USERNAME-HERE
```

## Upload a real package to the Python Package Index
* Choose a memorable and unique name for your package. You don’t have to append your username as you did in the tutorial.
* Register an account on https://pypi.org - note that these are two separate servers and the login details from the test server are not shared with the main server.
* Use twine upload dist/* to upload your package and enter your credentials for the account you registered on the real PyPI.
* Install your package from the real PyPI using python3 -m pip install [your-package].
