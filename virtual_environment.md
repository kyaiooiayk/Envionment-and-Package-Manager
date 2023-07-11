# 4 ways to create a virtual environment in Python
***

## Native
- Create virtual environmnet: `python -m venv you_venv_name`
- Make it executable: `chmod +x you_venv_name/bin/activate`
- Check the hidden file with: `ls -a` and see if the folder is there
- Activate: `source ./your_venv_name/bin.activate`
- Install dependencies: `pip install -r requirements.txt`
***

## Pyenv
- Check [this](https://akrabat.com/creating-virtual-environments-with-pyenv/) out
***

## Conda
- This assumed you have installed conda or miniconda in your system.
- See which conda you are using (meaning it shows the path of the executable being called): `which conda`
- Create a virtual environment using conda specific command: `conda create –-name my_env_name python=3.7` (check for the last stable Python realease [here](https://www.python.org/downloads/macos/))
- Activate the virtual environment: `conda activate my_env_name` 
- How to visualise all the env available: `conda env list`
- Install any package you like via these two options: `conda install package_name` or `pip package_name`
- How to delete a virtual env: `conda env remove --name=my_env_name`
***

## Poetry
- You have two options here:
  - Use an already existing virtual environment: `poetry env use <path_to_yout_virtual_env>`
  - USe the virtual environment poetry has creted for you. To get a list of those use: `poetry env info`
***
