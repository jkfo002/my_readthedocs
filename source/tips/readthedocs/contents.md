# readthedocs

## 配置总结

- 注册账号 (略)

- 本地构建

  > 基于python 3.12

  ```shell
  # 安装Sphinx（必须）
  pip3 install -U Sphinx
  mkdir my_readthedocs
  cd my_readthedocs
  sphinx-quickstart # 直接键入命令行
  make html
  ```

  一路回车，可选项见参考

  更改主题（可选）

  ```shell
  pip3 install sphinx_rtd_theme
  ```

  md支持（可选）

  ```shell
  pip3 install recommonmark
  ```

  配置`source/conf.py`

  ```python
  # Configuration file for the Sphinx documentation builder.
  #
  # For the full list of built-in configuration values, see the documentation:
  # https://www.sphinx-doc.org/en/master/usage/configuration.html
  
  # -- Project information -----------------------------------------------------
  # https://www.sphinx-doc.org/en/master/usage/configuration.html#project-information
  
  project = 'my_readthedocs'
  copyright = '2024, jkfo'
  author = 'jkfo'
  release = '0.1.1'
  
  # -- General configuration ---------------------------------------------------
  # https://www.sphinx-doc.org/en/master/usage/configuration.html#general-configuration
  
  extensions = []
  
  templates_path = ['_templates']
  exclude_patterns = []
  
  language = 'zh_CN'
  
  # -- Options for HTML output -------------------------------------------------
  # https://www.sphinx-doc.org/en/master/usage/configuration.html#options-for-html-output
  
  html_theme = 'alabaster'
  html_static_path = ['_static']
  
  ## add
  import sphinx_rtd_theme
  html_theme = "sphinx_rtd_theme"
  html_theme_path = [sphinx_rtd_theme.get_html_theme_path()]
  
  ## add
  extensions = [
      'recommonmark'
  ]
  ```

- github (略)

- 项目托管

  若需要项目托管的话，需要在github中添加`.readthedocs.yaml`

  ```yaml
  # Read the Docs configuration file for Sphinx projects
  # See https://docs.readthedocs.io/en/stable/config-file/v2.html for details
  
  # Required
  version: 2
  
  # Set the OS, Python version and other tools you might need
  build:
    os: ubuntu-22.04 # 不用管
    tools:
      python: "3.12"
      # You can also specify other tool versions:
      # nodejs: "20"
      # rust: "1.70"
      # golang: "1.20"
  
  # Build documentation in the "docs/" directory with Sphinx
  sphinx:
    configuration: source/conf.py # 更改为自己的路径，有的为docs
    # You can configure Sphinx to use a different builder, for instance use the dirhtml builder for simpler URLs
    # builder: "dirhtml"
    # Fail on all warnings to avoid broken references
    # fail_on_warning: true
  
  # Optionally build your docs in additional formats such as PDF and ePub
  # formats:
  #   - pdf
  #   - epub
  
  # Optional but recommended, declare the Python requirements required
  # to build your documentation
  # See https://docs.readthedocs.io/en/stable/guides/reproducible-builds.html
  python:
    install:
      - requirements: requirements.txt # 需要添加的python包
  ```

  `requirements.txt`为必须

  >sphinx_rtd_theme
  >recommonmark
  
- 更新

  本地更改后push到github就可以，readthedocs自动更新

## 参考

`https://readthedocs-demo-zh.readthedocs.io/zh-cn/latest/%E6%96%87%E4%BB%B6%E6%89%98%E7%AE%A1%E7%B3%BB%E7%BB%9F-ReadtheDocs.html#id1`

`https://blog.csdn.net/lu_embedded/article/details/109006380`