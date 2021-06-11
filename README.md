# python-tilt-warlock


```python
import warlock
import requests
import json
from datetime import datetime
from hashlib import sha256

tilt_schema = requests.get("https://raw.githubusercontent.com/Transparency-Information-Language/schema/master/tilt-schema.json").content
tilt_schema_dict = json.loads(tilt_schema)

Tilt = warlock.model_factory(tilt_schema_dict['properties']['meta'])

# lang = 'xyz' # crashes, because it is not a valid language code
lang = 'en'

document = Tilt(
    _id="0",
    name="Green Company",
    created=datetime.now().isoformat(), 
    modified=datetime.now().isoformat(),
    version=1,
    language=lang,
    status="active",
    url="https://example.com",
    _hash=sha256('rest_of_the_document'.encode('utf-8')).hexdigest())

print(document.name)

# Playin' around...
Tilt = {}
for p in tilt_schema_dict['properties'].keys():
    Tilt[p] = warlock.model_factory(tilt_schema_dict['properties'][p])


```
