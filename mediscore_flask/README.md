# Medi score flask app

## Overview

A web app that uses render, flask and the mediscore python program made earlier, to display the results of the program.

## How to run

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
python app.py
```

## app.py

### imports
```python
from flask import Flask, render_template,request, redirect, url_for,flash
import pickle
from flask_wtf import FlaskForm
from wtforms import SelectField
from forms import InputForm
from mediscore_function import calculate_medi_score
```

### create and configure flask app object
```python
app = Flask(__name__)

app.config['SECRET_KEY'] = 'Eight-Handled Sword Divergent Sila Divine General Mahoraga'

@app.route('/', methods=['GET', 'POST'])
```
### home() function
### setting visibility and getting form
```python
    print_mediscore = False

    form = InputForm()
```
### check form input and set variables
```python
    if form.validate_on_submit():
        resp_type = int(form.resp_type.data)
        conc = int(form.conc.data)
        resp_rate = form.resp_rate.data
        time_since = form.time_since.data
        spo2 = form.spo2.data
        temp = form.temp.data
        cbg = form.cbg.data
```
### get medi score and create flag variable
```python
        medi_score = calculate_medi_score(resp_type, conc, resp_rate, spo2, temp, cbg, time_since)

        alert = False
```

### check return type, to check for errors and choose what to display
```python
        if isinstance(medi_score[0],int):
            alert = medi_score[1]
            medi_score = "The patient's Medi score is "+str(medi_score[0])+"."
        print_mediscore = True
```
### send data to page
```python
      return render_template('home.html', form=form,flag=print_mediscore,medi_score=medi_score,alert=alert)

  return render_template('home.html', form=form)
```
### Screenshots

Healthy patient

![Healthy patient's medi score](/mediscore_flask/screenshots/healthy_patient.png?raw=true)

Condition worsening

![Change in medi score](/mediscore_flask/screenshots/mediscore_change.png?raw=true)

Input error

![Input error](/mediscore_flask/screenshots/input_error.png?raw=true)

