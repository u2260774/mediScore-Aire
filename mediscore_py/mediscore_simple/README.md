### history.json

Stores the previous scores of the patient in the following format:

bash
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


### mediscore.py 

The main file, containing the functions necessary for handling and converting observations to scores.
