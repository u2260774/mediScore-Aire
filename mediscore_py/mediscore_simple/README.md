### history.json

Stores the previous scores of the patient in the following format:

```bash
{
            "time": str(datetime.now()),
            "info": [
                {
                    "resp_type": resp_type,
                    "consc_type": consc_type,
                    "resp_rate_score": resp_rate_score,
                    "spo2_score": spo2_score,
                    "temp_score": temp_score,
                    "cbg_score": cbg_score,
                    "medi_score": medi_score,
                    "flag": flag
                }
            ]
        }
```

### mediscore.py 

The main file, containing the functions necessary for handling and converting observations to scores.

calculate_medi_score:

```python
def calculate_medi_score(respirationType, consc, respRate, spo2, temperature, cbg, timeSinceMeal):
    try:
        # check current time for flag
        curr_time = datetime.now()
        # assign mediscores
        resp_type = get_resp_type(respirationType)
        consc_type = get_consciousness(consc)
        resp_rate_score = get_resp_rate(respRate)
        spo2_score = get_spo2(spo2, resp_type)
        temp_score = get_temp(temperature)
        cbg_score = get_cbg(cbg, timeSinceMeal)
        # set default flag value
        flag = False
        # add everything up
        medi_score = resp_type + consc_type + resp_rate_score + spo2_score + temp_score + cbg_score
        # check if history file exists
        if os.path.isfile('history.json'):
            with open('history.json') as history:
                history_data = json.load(history)
                # get time and mediscore from last entry
                time = datetime.strptime(history_data["history"][-1]["time"], '%Y-%m-%d %H:%M:%S.%f')
                prev_score = history_data["history"][-1]["info"][0]["medi_score"]
                delta = curr_time - time
                # check if less than 24 hours and greater than 2 difference
                if delta.seconds / 86400 < 1 and medi_score - prev_score > 2:
                    flag = True
        # construct object to insert new data
        patient_info = {
            "time": str(datetime.now()),
            "info": [
                {
                    "resp_type": resp_type,
                    "consc_type": consc_type,
                    "resp_rate_score": resp_rate_score,
                    "spo2_score": spo2_score,
                    "temp_score": temp_score,
                    "cbg_score": cbg_score,
                    "medi_score": medi_score,
                    "flag": flag
                }
            ]
        }
        # check if file exists, create one if it doesn't
        if os.path.isfile('history.json') is False:
            with open('history.json', 'w') as history:
                history.write('{"history":[]}')
        # write new data
        with open("history.json", 'r+') as history:
            history_data = json.load(history)
            history_data["history"].append(patient_info)
            history.seek(0)
            json.dump(history_data, history, indent=4)
        # return mediscore and flag
        return medi_score, flag
    except Exception as e:
        return str(e)
```
