Travis is a [[Continuous Integration]] tool that builds and runs [[Testing|Tests]] on a remote server!


# Configuration
[Main Build Config Docs](https://config.travis-ci.com/)
If you already have a github account set up with travis-ci.com, add a `.travis.yml` file to the root of the repository.

## [Lifecycle](https://docs.travis-ci.com/user/job-lifecycle/#the-job-lifecycle)
1. `apt addons` - Optional
2. `cache components` - Optional
3. `before_install`
4. `install`
5. `before_script`
6. `script`
7. `before_cache` - If Caching enabled
8. `after_success` or  `after_failure`
9. `before_deploy` - if Deploy enabled
10. `deploy` - Optional
11. `after_deploy` - Optional
12. `after_script`

### Install
To install system dependencies:
```
before_install:
  - sudo apt -y install ...
```
Or use the [apt addon](https://docs.travis-ci.com/user/installing-dependencies/#installing-packages-with-the-apt-addon)
```yaml
addons:
  apt:
    sources:
	- ...
	packages:
	- ...
```
Or the [homebrew addon](https://docs.travis-ci.com/user/installing-dependencies/#installing-packages-on-macos)
```yaml
addons:
  homebrew:
    packages:
	- ..
	casks:
	- ..
```


```
install:
  - npm install
  - pip install .
```

### Build
```
script:
  - bundle exec rake build
```

## [Job Matrix](https://docs.travis-ci.com/user/customizing-the-build#build-matrix)
Some keys are special [matrix expansion keys](https://config.travis-ci.com/matrix_expansion) that create new jobs, their values running as the cross-product of all the other matrix expansion keys.

### Defining Specific Jobs
If you want to avoid build matrix...
```
language: ...
jobs: 
  include:
    - name "name of job"
      python: 3.7
	  os: ...
	  language: ..
    - name "other job"
      ...
```

### [OS](https://config.travis-ci.com/ref/os) / [Environment](https://docs.travis-ci.com/user/reference/overview/)
```
os:
- linux
- osx
- windows
```




### [Python](https://docs.travis-ci.com/user/languages/python/)
```yaml
language: python
python:
  - "3.7"
  - "3.8"
  - "3.9"
install:

script:
  - pytest
```
See [[Pytest]]


## Specify What/When to Build
### [Branches](https://docs.travis-ci.com/user/customizing-the-build#safelisting-or-blocklisting-branches)
Syntax:
```yaml
# blocklist
branches:
  except:
  - legacy
  - experimental

# safelist
branches:
  only:
  - master
  - stable

# build all
branches:
  only:
  - /.*/
```
You can also use regex :)



### Skipping
Add `[skip travis]` to the commit message.




### References
-  https://docs.travis-ci.com/user/tutorial/
- [Python docs](https://docs.travis-ci.com/user/languages/python/)
- [Customization/ travis.yml docs](https://docs.travis-ci.com/user/customizing-the-build)
- [Build Config Reference](https://config.travis-ci.com/)
