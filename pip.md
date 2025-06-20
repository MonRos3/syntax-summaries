# Python Package Manager - pip

Acronym for: pip install packages
This is a common and useful package manager. Don't forget to set up a virtual environment before bulk-installing packages to your machine.

Install pip:

```bash
pip3 install flask
```

Generate a requirements txt file:

```bash
pip freeze > requirements.txt
```

Install all packages listed in the requirements.txt document:

```bash
pip3 install -r requirements.txt
```

List installed packages:

```bash
pip list
```

List installed packages in the same format as the requirements.txt document:

```bash
pip list --format=freeze > requirements.txt
```

Uninstall all pip packages:

```bash
pip uninstall -y -r <(pip freeze)
```
