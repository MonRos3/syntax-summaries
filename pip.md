# Python Package Manager - pip
Acronym for: pip install packages

pip3 install flask

pip freeze > requirements.txt		//generates a requirements txt file
pip3 install -r requirements.txt
pip list --format=freeze > requirements.txt
pip list 			//lists installed packages
pip uninstall -y -r <(pip freeze)		//uninstall all pip packages

