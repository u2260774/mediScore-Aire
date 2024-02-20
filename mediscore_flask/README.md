# Medi score flask app

## Overview

A web app that uses render, flask and the mediscore python program made earlier, to display the results of the program.

## Steps to Run the Application

### 1. Clone the Repository

```bash
git clone https://github.com/u2260774/medi_score_flask.git
cd medi_score_flask
```

### 2. Set Up a virtual environment 

venv (Python 3.10)
```bash
python3.10 -m venv myenv
source myenv/bin/activate
```

conda (Python 3.10)
```bash
conda create --name myenv python=3.10
conda activate myenv
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run application

```bash
flask --app app run
``
